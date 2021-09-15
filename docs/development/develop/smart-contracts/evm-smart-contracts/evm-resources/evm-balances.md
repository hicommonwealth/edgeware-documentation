# EVM Balances

The "EVM" module in Substrate provides support for executing Ethereum contracts on a substrate chain. In order to perform any gas or balance-related actions on the EVM, the calling account must have a balance. How do these balances work?

## Balance Conversion

In order to use Ethereum contracts on a Substrate chain, the chain must have a protocol to support the following assumptions:

1. A \(32-byte\) Substrate address must have a corresponding \(20-byte\) Ethereum address.
2. Each \(20-byte\) Ethereum address must have its balance maintained.

The EVM module satisfies step 1 by simply truncating the source Substrate address into an Ethereum address, taking the first 20 bytes. To satisfy step 2, the chain uses the pre-existing Substrate balances module to manage each Ethereum address, by converting Ethereum addresses back into "EVM addresses", which are 32-byte Substrate addresses. **Note that these EVM addresses have no inherent relationship to the original truncated Substrate address.**

Let us take an example:

* Consider a 32-byte Substrate address: `0x1234567890ABCDEF1234567890ABCDEF1234567890ABCDEF1234567890ABCDEF`.
* Truncate this to create a 20-byte Ethereum address: `0x1234567890ABCDEF1234567890ABCDEF12345678`
* This Ethereum address's balance comes from the Substrate balances module's state for its corresponding EVM address, produced by hashing the above bytes with an `evm:` prefix \(`0x65766D3A`\). So we perform `Hash(0x65766D3A1234567890ABCDEF1234567890ABCDEF1234)` = `0xAF8536395A1EEC8EDA6FB9CF36739ECF75BECF6FEA04CEEC108BBB6AA15B7CB3`, whose balance in the Balances module will be used for EVM-related operations.
  * The exact hash function used is defined in the Substrate chain's runtime file. In Edgeware's case, the hashing algorithm is `Blake2`, but the `Keccak` is also a possibility.

**Note that these actions are not reversible: we cannot convert from an EVM address back to its Ethereum address, nor can we convert from an Ethereum address back to its "source" Substrate address.**

## Managing Ethereum Balances on Substrate

Two operations are possible: we can "deposit" funds from a Substrate account into its corresponding Ethereum account, and we can "withdraw" funds from an Ethereum account back into the source Substrate account.

### Deposits

Since the EVM address backing an Ethereum address is computed determinstically, as above, we can perform a standard balance transfer from our source Substrate account to the EVM address in order to seed the Ethereum account with funds.

This can be performed by calling `balances::transfer(prefixAndHash(truncate(account)).signAndSend(account)`, where `account` is the source substrate account, `truncate` takes the first 20 bytes as the Ethereum address, and `prefixAndHash` applies the `evm:` prefix and takes the hash as to convert back into a 32-byte Substrate address.

### Withdrawal

Since the EVM address is computed deterministically, we do not have a private key for it, so we cannot perform a balance transfer from it via normal means. As a result, the EVM module provides a special function `withdraw` for transferring funds back from an Ethereum account to the source Substrate account.

This can be performed by calling `evm::withdraw(truncate(account), value).signAndSend(account)` where `account` is the source Substrate account, and `truncate` takes the first 20 bytes as the Ethereum address.

### Ethereum Balances

Ethereum balances are handled as if they were running on any Ethereum chain: gas is subtracted from the balance \(the quantity of gas used can be accessed from the transaction receipt returned by the EVM module through web3 or truffle\), and transfers work as expected.

The balance of the 20-byte Ethereum address and the 32-byte EVM address should be identical, when compared: `web3.eth.getBalance(ethAddress)` should equal `system::balances(prefixAndHash(ethAddress)).freeBalance`, where `ethAddress` is the 20-byte Ethereum address, and `prefixAndHash` applies the `evm:` prefix and takes the hash, as explained above.

**Note that the conversion rate of EVM gas to substrate tokens is defined in the Substrate runtime as `FeeCalculator`, which in Edgeware's case is set to a 1-to-1 wei-to-Substrate token mapping.**

When converting, also note the `gasPrice` is specified in the EVM call, as the conversion factor from the `gasUsed` field in the receipt to wei.

\(beneath is the original technical writeup\)

### Addresses:

* Convert a Substrate address to a EVM address: `address[0..20]` — take the first 20 bytes.
* Convert an EVM address into a Substrate address: add `evm:` prefix to data, and take the hash. **THIS IS NOT REVERSIBLE**.
  * See: [https://gitlab.parity.io/parity/substrate/-/blob/16fdfc4a80a14a26221d17b8a1b9a95421a1576c/frame/evm/src/lib.rs\#L167](https://gitlab.parity.io/parity/substrate/-/blob/16fdfc4a80a14a26221d17b8a1b9a95421a1576c/frame/evm/src/lib.rs#L167)

    ```text
    fn into_account_id(address: H160) -> AccountId32 {
        let mut data = [0u8; 24];
        data[0..4].copy_from_slice(b"evm:");
        data[4..24].copy_from_slice(&address[..]);
        let hash = H::hash(&data);

        AccountId32::from(Into::<[u8; 32]>::into(hash))
    }
    ```
* **Effectively: each Substrate address is mapped to a specific EVM address, which is** _**maintained as if it were a Substrate address**_ **\(see below\)**_**.**_ **I call the \(32-byte\) Substrate address created from a \(20-byte\) EVM address the "substrate-ethereum equivalent".**
  * As an example, consider the \(fake\) 32-byte Substrate address \(it uses an `AccountId32` which is an array `[u8, 32]`, represented here as a 64 char hex string\): `0x1234567890ABCDEF1234567890ABCDEF1234567890ABCDEF1234567890ABCDEF`
  * We first convert this to a 20-byte EVM address \(represented here as a 40 char hex string\): `0x1234567890ABCDEF1234567890ABCDEF1234`
  * We then convert that into a new substrate address: `Hash('evm:'+0x1234567890ABCDEF1234567890ABCDEF1234)` = `Hash(0x65766D3A1234567890ABCDEF1234567890ABCDEF1234)`, where `Hash` is defined in the runtime as either Blake or Keccak. Edgeware uses Blake \(see: [https://github.com/hicommonwealth/edgeware-node/blob/edg-frontier-up-1/node/runtime/src/lib.rs\#L857](https://github.com/hicommonwealth/edgeware-node/blob/edg-frontier-up-1/node/runtime/src/lib.rs#L857)\), so the final output would be, in hex: `0xAF8536395A1EEC8EDA6FB9CF36739ECF75BECF6FEA04CEEC108BBB6AA15B7CB3`
  * Thus, the 32-byte "substrate account" `0x12345...` maps to the 20-byte "ethereum account" `0x12345...1234` which maps to the 32-byte "substrate-ethereum equivalent" `0xAF8536...` which functions as a valid Substrate address. **This is the Substrate address used to maintain account balances for the corresponding EVM account.**

### Balances:

* An EVM address can be given a balance at genesis, or by sending balance directly to the "substrate-ethereum equivalent" as one would normally send balance between accounts.

  > "it seems one cannot use native substrate addresses by default to interact with the EVM, can you expand on this more? What does a user have to. do if they have 0 balance at genesis"

  * Each substrate address is deterministically mapped to an EVM address.

    * There is a util in frontier `evm-address.js` which purports to perform this conversion, but doesn't seem to do it correctly based on the updated evm pallet \(the util hasn't been updated in 4 months\)
    * See implementations of the following utils in the frontier-tester project: [https://github.com/hicommonwealth/frontier-tester/blob/master/utils.js\#L46](https://github.com/hicommonwealth/frontier-tester/blob/master/utils.js#L46)
    * It is doable as follows:

    ```text
    import { decodeAddress } from '@polkadot/util-crypto';

    const convertToEvmAddress = (substrateAddress) => {
      const addressBytes = decodeAddress(substrateAddress);
      return '0x' + Buffer.from(addressBytes.subarray(0, 20)).toString('hex');
    }
    ```

    * In Rust \(there is probably a simpler way to do this with refs\):

    ```text
    fn convertToEvmAddress(address: H256) -> H160 {
      let mut evmAddress: [u8; 20] = Default::default();
        evmAddress[0..20].copy_from_slice(&address[0..20]);
        evmAddress
    }
    ```

    * **The original substrate address cannot be recovered from the EVM address alone.**

  * Each EVM address is deterministically mapped to another substrate address which maintains its balance, and which can be sent funds directly via a basic transfer. This substrate address is computable as follows:

    ```text
    import { encodeAddress, blake2AsHex } from '@polkadot/util-crypto';

    const convertToSubstrateAddress = (evmAddress, prefix = 42) => {
      const addressBytes = Buffer.from(evmAddress.slice(2), 'hex');
      const prefixBytes = Buffer.from('evm:');
      const convertBytes = Uint8Array.from(Buffer.concat([ prefixBytes, addressBytes ]));
      const finalAddressHex = blake2AsHex(convertBytes, 256);
      return encodeAddress(finalAddressHex, prefix);
    }
    ```

    * In Rust:

    ```text
    fn convertToSubstrateAddress(address: H160) -> AccountId32 {
        HashedAddressMapping<BlakeTwo256>::into_account_id(address)
    }
    ```

  * **This generated substrate address is equivalent to the EVM address for all intents and purposes, and is a deterministic computation from the original substrate address — it can be used in other pallets freely as a "proxy" for the EVM address. However, it does not have a private key, so it cannot sign.**

* Funds must be withdrawn from an EVM account via the `pallet_evm::withdraw` function, as the "substrate-ethereum equivalent" does not have a known private key from which to send transactions.
  * [https://github.com/paritytech/substrate/blob/master/frame/evm/src/lib.rs\#L304](https://github.com/paritytech/substrate/blob/master/frame/evm/src/lib.rs#L304)
  * The caller must provide the \(20-byte\) EVM address that corresponds to their Substrate address — this is checked here: [https://github.com/paritytech/substrate/blob/master/frame/evm/src/lib.rs\#L148](https://github.com/paritytech/substrate/blob/master/frame/evm/src/lib.rs#L148).
  * The function converts that EVM address into the "substrate-ethereum equivalent", from which it transfers the funds.
* The `free_balance` of the "substrate-ethereum equivalent" is used as the balance of the ethereum account: [https://github.com/paritytech/substrate/blob/master/frame/evm/src/lib.rs\#L471](https://github.com/paritytech/substrate/blob/master/frame/evm/src/lib.rs#L471)
* Mutations to the ethereum account's balance, such as after execution, either call `slash` or `deposit_creating` on the "substrate-ethereum equivalent" depending on whether balance was added or removed: [https://github.com/paritytech/substrate/blob/master/frame/evm/src/lib.rs\#L440](https://github.com/paritytech/substrate/blob/master/frame/evm/src/lib.rs#L440)
* **For a Javascript example of balances in action, see this test file in frontier-tester:** [**https://github.com/hicommonwealth/frontier-tester/blob/master/web3tests/testSubstrateBalances.ts**](https://github.com/hicommonwealth/frontier-tester/blob/master/web3tests/testSubstrateBalances.ts)

### Gas:

* The prices of various functions in gas are defined in the `EVM_CONFIG` in the runtime.
  * Edgeware's current configuration uses a clone of the `ISTANBUL` config, with the CreateContractLimit raised.
  * See: [https://github.com/rust-blockchain/evm/blob/master/runtime/src/lib.rs\#L245](https://github.com/rust-blockchain/evm/blob/master/runtime/src/lib.rs#L245)
* The conversion rate of gas to substrate tokens is defined in the runtime as `FeeCalculator`, which in Edgeware's case is set to a 1-to-1 mapping.
* Gas is "withdrawn" from the StackExecutor before execution: [https://github.com/paritytech/substrate/blob/master/frame/evm/src/lib.rs\#L608](https://github.com/paritytech/substrate/blob/master/frame/evm/src/lib.rs#L608)
* Balance changes including gas \(performed by the above withdraw\) are written back to the "substrate-ethereum equivalent"'s balance once the EVM execution has been `apply`ed on the backend: [https://github.com/paritytech/substrate/blob/master/frame/evm/src/backend.rs\#L144](https://github.com/paritytech/substrate/blob/master/frame/evm/src/backend.rs#L144)

