# Set Up a Validator

Welcome to the official, in-depth Edgeware guide to validating. We're happy that you're interested in validating on Edgeware and we'll do our best to provide in-depth documentation on the process below. As always, reach out on [Discord](https://discord.gg/mYk543EXBV) or [Telegram](https://t.me/heyedgeware) if you have questions about the project.

This document contains all the information one should need to start validating on Edgeware using the **command line interface**. We will start with how to setup one's node and proceed to how to key management and monitoring. To start, we will use the following terminology of keys for the guide:

* _**stash**_ - the stash keypair is where most of your funds should be located. It can be kept in cold storage if necessary.
* _**controller**_ - the controller is the keypair that will control your validator settings. It should have a smaller balance, e.g. 10-100 EDG
* _**session**_ - the 4 session keypairs are hot keys that are stored on your validator node. They do not need to have balances.

## Requirements

1. You will need 6 keypairs: a `stash` \(ed25519 or sr25519\), `controller` \(ed25519 or sr25519\), and 4 `session` \(3 ed25519 and 1 sr25519\) keypairs. You can generate these using the `subkey` utility. We will be using derived keys in the examples, if you do not use derived keys, simply input the seed/mnemonic needed to sign from these accounts.
2. Aura keys \(ed25519\)
3. Grandpa keys \(ed25519\)
4. ImOnline keys \(ed25519\)
5. AuthorityDiscovery keys \(sr25519\)
6. You will need at least the existential balance \(1,000,000,000,000,000 token units i.e 0.0001 EDG\) in both the `stash` and `controller` accounts plus the balances needed to send transactions from these accounts.
7. You will need a live, fully-synced Edgeware node running with the `--validator` flag that has set one's session keys, either before or after you complete the onboarding process.

## Pre-requisites

* First follow the guide in the [README.md](https://github.com/hicommonwealth/edgeware-node/blob/master/README.md) for installing and running the `edgeware-node`.
* Download from source or from the `npm` registry the `edgeware-cli` located [here](https://github.com/hicommonwealth/edgeware-cli/).

  Note: `edgeware-cli` has several dependencies [viewable here.](https://www.npmjs.com/package/edgeware-cli)

* Install `subkey` as well if you do need to generate new keypairs:

  cargo install --force --git [https://github.com/paritytech/substrate](https://github.com/paritytech/substrate) subkey

From this point on, we will assume you are familiar with using `subkey`, if that is not the case, you can read about the `subkey` commands [here](https://github.com/paritytech/substrate/blob/master/bin/utils/subkey/README.md).

## Onboarding

1. First, create the _**stash**_ and _**controller**_ keypairs using `subkey`. You can also **optionally** \*\*create your 4 session keys. Create ED25519 keypairs using `-e` flag with subkey.
2. Next, you will need to bond from your _**stash**_ keypair to your _**controller**_ keypair. Using the CLI and a local node, you will run:

   ```text
   edge -s <STASH_SEED> staking bond <CONTROLLER_B58_ADDRESS> <AMOUNT> <REWARD_DESTINATION>
   ```

3. The _**stash**_ seed should be a mnemonic + derivation path for your _**stash**_ keypair
4. The _**controller**_ address should be a Base58 encoded public key \(starts with a 5\)
5. The bond _**amount**_ should be an integer balance in units of EDG
6. The _**reward destination**_ is where rewards will go; the options are `stash`, `controller`, and `staked` \(where staked adds rewards to the amount staked\)
7. Next, you will need to set your validator preferences from your _**controller**_ account. Using the CLI and a local node, you will run:

   ```text
   edge -s <CONTROLLER_SEED> staking validate <COMMISSION_PERCENTAGE>
   ```

8. The _**controller**_ seed should be a mnemonic + derivation path for your _**controller**_ keypair
9. The _**unstake threshold**_ is the number of times your node is offline before dropping out
10. The _**commission percentage**_ is the percentage of rewards you will 
11. Next, you will need to set your _**session**_ keys from your _**controller**_ keypair. Using the CLI and a local node, you will run:

    ```text
    edge -s <CONTROLLER_SEED> session setKeys <OUTPUT_FROM_ROTATE_KEYS> 0x
    ```

12. The _**controller**_ seed should be a mnemonic + derivation path for your _**controller**_ keypair
13. The _**session**_ public keys should be concatenated from the output of the rotate keys rpc command.

### Examples of all the commands are below:

In the following, we have downloaded and compiled `edgeware-cli` from source to yield a `/bin/edge` binary. You can use `tsc` to do so if you compile from source.

```text
edge -s "axis service this custom because top clap sock weekend tenant vehicle merge" staking bond 10 stash // bond 10 EDG (10 * 10^18 currency units)

edge -s "axis service this custom because top clap sock weekend tenant vehicle merge" session setKeys 0fea2a18acbd19e4a21c3ae29ecefee61d32d46dc4b9a9c5ccecbbbdff7b0a7e8e55bd3035d18f40d8dd1b5d940c47066ddb6f37ec7261d69121e8353d612d1410f7b7f954b3225b148c5de650e0bc3c941ae65e1557c3805c3b0df37285c3892cc2f99d97254ffdf1640c29dff2c6272dbf4dc8dedb46e43ba0bd12ab269b3c 0x // set session keys to the 4 concatentated keys submitted

edge -s "axis service this custom because top clap sock weekend tenant vehicle merge" staking validate 10 // set validator preferences to 10% commission
```

## Validating

The v099 testnet requires validators to manage 4 validating keys for the Aura, Grandpa, ImOnline, and AuthorityDiscovery modules.

1. Aura keys \(ed25519\)
2. Grandpa keys \(ed25519\)
3. ImOnline keys \(ed25519\)
4. AuthorityDiscovery keys \(sr25519\)

Now while running your full node to sync or afterward, you can start to set up your session keys for the node. The command for inserting keys and rotating keys is the same as it has been. To rotate new session keys, run the following while your node is running:

```text
curl -H 'Content-Type: application/json' --data '{ "jsonrpc":"2.0", "method":"author_rotateKeys", "id":1 }' 127.0.0.1:9933
```

To insert existing session keys, you can run for each key the following command while your node is running:

```text
curl -H 'Content-Type: application/json' --data '{ "jsonrpc":"2.0", "method":"author_insertKey", "params":["KEY_TYPE", "SEED", "PUBKEY_HEX"],"id":1 }' localhost:9933
```

The four key types you will enter individuals are:

* `aura` for Aura keys
* `gran` for Grandpa keys
* `imon` for ImOnline keys
* `audi` for AuthorityDiscovery keys

After running these `curl` commands, you should receive as output from `stdout` the public keys you provided \(or didn't\) in a JSON string. That also means the process was a success! You should now see yourself in the list of newly/pending validators to go into effect in future sessions. In the next era \(up to 1 hour\), if there is a slot available, your node will become an active validator.

