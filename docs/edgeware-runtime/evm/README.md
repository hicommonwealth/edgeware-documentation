# EVM

Edgeware has a pallet that allows developers to write EVM smart-contracts. This means that you can use Edgeware as you would with Ethereum. Edgeware is fully compatible with Ethereum's Web3 API and EVM. Here, we'll walk through a few subtle differences between Edgeware and Ethereum. Namely, Edgeware has a Proof of Stake-based consensus mechanism. This shouldn't affect you if you're building a DeFi or NFT based application. See our related documentation on [proof-of-stake](https://docs.edgewa.re/edgeware-runtime/consensus). In the following sections we detail Edgeware&lt;&gt;EVM Compatibiltiy.

## Full-Ethereum API and Tooling Compatibility

If you're moving some portion of your smart contracts, state, or considering porting your full set of contracts off Ethereum to Edgeware, it should 'just work'. That is the full set of your application, contracts, and tooling will remain the same. Edgeware will be able to support:

* Solidity and Serpent Based Smart Contracts
* Ecosystem Tools \(e.g., block explorers, front-end development libraries, wallets--i.e Metamask\)
* Development Tools \(e.g., Truffle, Remix, MetaMask, ethers, web3js, truffle\)
* Ethereum Tokens via Bridges \(e.g., token movement, state visibility, message passing\)

You can view our [tutorials](https://contracts.edgewa.re) to get a better feel for building Ethereum smart contracts on Edgeware, and how to directly offload or migrate your Ethereum application onto Edgeware.

As previously mentioned, Edgeware is proof of stake, this does mean that smart contracts that rely on components of Ethereum's API that touch on Proof of Work--difficulty, uncles, hashrate won't work as expected on Edgeware. For those values, we have constant values set at the runtime level. Existing Ethereum contracts that rely on Proof of Work internals \(e.g., mining pool contracts\) will almost certainly not work as expected on Edgeware.

## How Edgeware achieves Ethereum Compatibility

Edgeware achieves Ethereum compatibility in three integrated components. If you're a smart contract developer, this may just be of passing interest.

* Pallet Ethereum: which allows for full Ethereum Block Processing
* SputnikEVM: You can view the full Documentation here: [https://docs.rs/evm/](https://docs.rs/evm/)
* Pallet EVM: which allows you to deploy

