# WASM Contract Pallet

## WASM Contract Pallet

### WebAssembly \(Wasm\)

WebAssembly is used in Polkadot, Substrate and Edgeware as the compilation target for the runtime.

### What is WebAssembly?

WebAssembly, shortened to simply Wasm, is a binary instruction format for a stack-based virtual machine. Wasm is designed as a portable target for compilation of high-level languages like C/C++/Rust, enabling deployment on the web for client and server applications.

### Why WebAssembly?

WebAssembly is a platform agnostic binary format, meaning that it will run the same instructions across whatever machine it is operating on. Blockchains need determinancy in order to have reliable state transition updates across all nodes in the peer-to-peer network without forcing every peer to run the same exact hardware. Wasm is a nice fit for reliability among the possibly diverse set of machines. Wasm is both efficient and fast. The efficiency means that it can be uploaded onto the chain as a blob of code without causing too much state bloat while keeping its ability to execute at near-native speeds.

### Contracts Pallet

The Contracts pallet provides the ability for the runtime to deploy and execute WebAssembly \(Wasm\) smart contracts.

### Wasm Engine

The Contracts pallet depends on a Wasm sandboxing interface defining the Wasm execution engine available within the runtime. This is currently implemented with wasmi, a Wasm interpreter.

### Features

The Contracts module has a number of familiar and new features for the deployment and execution of smart contracts.

### Account Based

The Contracts module uses an account-based system similar to many existing smart contract platforms. To the Substrate runtime, contract accounts are just like normal user accounts; however, in addition to an AccountID and Balance that normal accounts have, a contract account also has associated contract code and some persistent contract storage.

### Two Step Deployment

Deploying a contract with the Contracts module takes two steps:

### Store the Wasm contract on the blockchain.

Instantiate a new account, with new storage, associated with that Wasm contract. This means that multiple contract instances, with different constructor arguments, can be initialized using the same Wasm code, reducing the amount of storage space needed by the Contracts module on your blockchain.

### Runtime Environment Types

For writing contracts and interacting with the runtime, a set of types are available \(e.g. AccountId, Balance, Hash, Moment\). These types can be user defined for custom runtimes, or the supplied defaults can be used.

### Contract Calls

Calls to contracts can alter the storage of the contract, create new contracts, and call other contracts. Because Substrate provides you with the ability to write custom runtime modules, the Contracts module also enables you to make asynchronous calls directly to those runtime functions on behalf of the contract's account.

### Sandboxed

The Contracts module is intended to be used by any user on a public network. This means that contracts only have the ability to directly modify their own storage. To provide safety to the underlying blockchain state, the Contracts module enables revertible transactions, which roll back any changes to the storage by contract calls that do not complete successfully.

### Gas

Contract calls are charged a gas fee to limit the amount of computational resources a transaction can use. When forming a contract transaction, a gas limit is specified. As the contract executes, gas is incrementally used up depending on the complexity of the computation. If the gas limit is reached before the contract execution completes, the transaction fails, contract storage is reverted, and the gas fee is not returned to the user. If the contract execution completes with remaining gas, the excess is returned to the user at the end of the transaction.

The Contracts module determines the gas price, which is a conversion between the Substrate Currency and a single unit of gas. Thus, to execute a transaction, a user must have a free balance of at least gas price \* gas limit which can be spent.

### Storage Rent

Similar to how gas limits the amount of computational resources that can be used during a transaction, storage rent limits the footprint that a contract can have on the blockchain's storage. A contract account is charged proportionally to the amount of storage its account uses. When a contract's balance goes below a defined limit, the contract's account is turned into a "tombstone" and its storage is cleaned up. A tombstone contract can be restored by providing the data that was cleaned up when it became a tombstone as well as any additional funds needed to keep the contract alive.

## Contracts Module vs EVM

The Contracts module iterates on existing ideas in the smart contract ecosystem, particularly Ethereum and the EVM.

The most obvious difference between the Contracts module and the EVM is the underlying execution engine used to run smart contracts. The EVM is a good theoretical execution environment, but it is not very practical to use with modern hardware. For example, manipulation of 256 bit integers on modern architectures is significantly more complex than standard types. Even the Ethereum team has investigated the use of [Wasm](https://github.com/ewasm/design) for the next generation of the network.

The EVM charges for storage fees only at the time of storage. This one-time cost results in some permanent amount of storage being used on the blockchain, forever, which is economically unsound. The Contracts module attempts to repair this through [storage rent](https://substrate.dev/docs/en/knowledgebase/smart-contracts/contracts-pallet#storage-rent) which ensures that any data that persists on the blockchain is appropriately charged for those resources.

The Contracts module chooses to approach contract creation using a [two-step process](https://substrate.dev/docs/en/knowledgebase/smart-contracts/contracts-pallet#two-step-deployment), which fundamentally changes how contracts are stored on chain. Contract addresses, their storage, and balances are now separated from the underlying contract logic. This could enable behavior like what [create2](https://eips.ethereum.org/EIPS/eip-1014) provided to Ethereum or even enable repairable or upgradeable contracts on a Substrate based blockchain.

### Resources

* [WebAssembly.org](https://webassembly.org/) - WebAssembly homepage that contains a link to the spec.
* [Wasmi](https://github.com/paritytech/Wasmi) - WebAssembly interpreter written in Rust.
* [Parity Wasm](https://github.com/paritytech/parity-Wasm) - WebAssembly serialization/deserialization in Rust.
* [Wasm utils](https://github.com/paritytech/Wasm-utils) - Collection of Wasm utilities used in Parity and Wasm contract development.
* [Pallet-contracts](https://crates.io/crates/pallet-contracts) - The Contract module provides functionality for the runtime to deploy and execute WebAssembly smart-contracts.
* [Contracts Pallet](https://substrate.dev/docs/en/knowledgebase/smart-contracts/contracts-pallet)

