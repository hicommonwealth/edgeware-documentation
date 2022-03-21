# Ecosystem Tools

### Chain Interfaces

* [Commonwealth](https://Commonwealth.im)
* [Polkadot UI](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fmainnet1.edgewa.re#/explorer)

## Polkadot UI

The [Polkadot UI](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fmainnet1.edgewa.re#/explorer) is an essential l interface for performing a variety of actions on Edgeware and Substrate-based chains. It will be the primary way that you interact with the Edgeware network, whether that is staking, account transactions, some governance functions, or more.

Secondary to the Polkadot UI is [Commonwealth.im](http://Commonwealth.im), which combines discussion and polling on-chain with governance and account functions. As Commonwealth is still under development, many instructions on this site will be written for Polkadot UI.

**Features**

* Manage accounts, view account info.
* Send and receive/monitor transactions
* View chain, block and node info.
* Conduct staking, democracy, council and treasury actions.
* View chain state and parameters.
* Observe extrinsics
* Upload contracts

### Wallets

* [**Commonwealth.im**](http://commonwealth.im/) **\(Sign-up in right top side, must connect EDG address\)** 
  * At this time,  **the wallet is under development**. It supports viewing balances, sending and receiving transactions, and governance actions via the Commonwealth.im UI. The public addresses shown do not display the Edgeware network ID-encoded version at this time, but this feature is due by end-of-launch-week. You should regenerate your public address using the link below. 
* [**Polkadot JS Browser Extension** ](https://github.com/polkadot-js/extension)**\(**[**Chrome**](https://chrome.google.com/webstore/detail/polkadot%7Bjs%7D-extension/mopnmbcafieddcagagdcbnhejhlodfdd) **and** [**Firefox**](https://addons.mozilla.org/en-US/firefox/addon/polkadot-js-extension/)**\)**  
  * Can be used to connect EDG addresses to Commonwealth.im. \(This is the Official Polkadot Wallet Extension\)
  * Supports the most features via[ the Polkadot UI.](https://polkadot.js.org/apps/#/explorer)
  * The Polkadot.js Browser Extension **does not display the Edgeware network ID encoded at this time.** The public address of your EDG wallet shown in the extension is encoded using the 'default network ID' of Subkey, the program that generates keypairs for Substrate-based chains. As a result, the public addresses shown may not be useful for using block explorers. You should regenerate your public key to derive the Edgeware network-ID-encoded public address, see above.
* [MathWallet Browser Extension](https://www.mathwallet.org/en/)
* [Polkawallet](https://polkawallet.io/) - A mobile wallet for Polkadot on both iOs and Android. Currently in development but a Beta version is available for download. Follow development on [GitHub](https://github.com/polkawallet-io/polkawallet-RN).
* [Enzyme](http://blockxlabs.com/) - Browser extension wallet. Follow development on [GitHub](https://github.com/blockxlabs/enzyme/).
* [Sakura ](https://github.com/w3finance/sakura)- Desktop Wallet for Polkadot Ecosystem. In development.
* [Signer](https://www.parity.io/signer/)                          
* [Lunie](https://lunie.io/)                                       
* [Trust Wallet](https://trustwallet.com/)                         
* [ImToken](https://token.im/)                                     
* [Ownbit](https://ownbit.io/)                                     
* [AirGap](https://airgap.it/)                                     
* [SafePal](https://www.safepal.io/download)                        
* [Crypto.com](https://crypto.com/en/index.html)                    
* [Ledger App](https://zondax.ch/kusama.html#overview)              
* [Atomic Wallet](https://atomicwallet.io)                          
* [Dether](https://dether.io/)                                      
* [Cobo Wallet](https://cobo.com/)                                  
* [Swipe](https://swipe.io/)                                         
* [Polkadot{.js} extension](https://github.com/EthWorks/extension)   
* [MetaMask](https://metamask.io/)                         
* [Speckle](https://github.com/GetSpeckle/speckle-browser-extension) 
* [KodaDot](https://kodadot.netlify.app/#/accounts)                  
* [Subwallet](https://github.com/yxf/subwallet)                      
* [Fearless](https://soramitsu.co.jp/fearless)                       
* [Spatium](https://spatium.net/)                                    
* [Blockchain.com](https://www.blockchain.com/)                      


### Nodes and Deployment

* [Gantree Infrastructure Toolkit for Substrate](https://github.com/gantree-io/gantree-lib-nodejs)
* [Polkalert: Node Monitoring](https://polkalert.com/)
* [Telemetry: Node Stats](https://telemetry.polkadot.io/)

### Block Explorers

* [Polkadot-JS Apps Explorer](https://polkadot.js.org/apps/#/explorer) - Polkadot dashboard block

  explorer. Currently connects to Kusama by default, but can be configured to connect to other

  remote or local endpoints.

* [Polkascan](https://polkascan.io/) - Blockchain explorer for Polkadot, Kusama, and other related

  chains. [Repo](https://github.com/polkascan/polkascan-os).

* [Subscan](https://subscan.io) - Blockchain explorer for Substrate chains.

  [Repo](https://github.com/itering/subscan-essentials).

### WASM

Webassembly related tools and projects.

* [ink!](https://github.com/paritytech/ink/) - an eDSL to write WebAssembly based smart contracts

  using the Rust programming language.

* [parity-wasm](https://github.com/paritytech/parity-wasm) - Low-level WebAssembly format library.
* [wasm-utils](https://github.com/paritytech/wasm-utils) - Collection of WASM utilities used in

  pwasm-ethereum and substrate contract development.

* [wasmi](https://github.com/paritytech/wasmi) - a Wasm interpreter conceived as a component of

  parity-ethereum \(ethereum-like contracts in wasm\) and substrate.

### Smart Contract tooling

* [Halva](https://github.com/halva-suite/halva) - a Truffle-inspired local development environment

  for Substrate.

* [Redspot](https://github.com/patractlabs/redspot)

### Faucets

* [BlockX Labs testEDG Faucet ](https://faucets.blockxlabs.com/)

### Grant Programs

* [Edgeware Grant Program](https://commonwealth.im/edgeware/proposal/discussion/466-creating-edgeware-grants)
* [Web3Foundation Grant Program](https://web3.foundation/grants/)

### API Feeds

* [Total Supply Endpoint for Edgeware](https://edgeware-supply.now.sh/) \(Does not subtract Treasury stash\)

### Key Generation and Conversion

* [Original Edgeware Key Generator for Lockdrop and Pub Key Convertor](https://edgewa.re/keygen/)
* [Subkey: Key Generation for Substrate Chains ](https://docs.substrate.io/v3/tools/subkey/#generating-keys)

### Node-as-a-Service Providers

These providers have not been vetted by the core development team.

| Name | Link to Product |
| :--- | :--- |
| BisonTrails | [https://bisontrails.co/edgeware/](https://bisontrails.co/edgeware/) |

_The following have announced they intend to develop NAAS._

* Ankr.com
* Stake.Fish
* [https://deploy.radar.tech/](https://deploy.radar.tech/)

## Network Monitoring & Reporting

* [Polkadot Telemetry Service](https://telemetry.polkadot.io/) - Network information including what

  nodes are running the chain, what software versions they are running, sync status, and location.

* Polkabot - Polkadot network monitoring and reporting using Matrix \(Riot / Element\) chat. Users may

  create custom bot plugins. [Blogpost](https://medium.com/polkadot-network/polkabot-a3dba18c20c8).

* [Ryabina's Telegram Bot](https://github.com/Ryabina-io/substratebot) - a Telegram bot for

  monitoring on-chain events of Substrate chains.

  [Github Repository](https://gitlab.com/Polkabot/polkabot)

* [PolkaStats](https://polkastats.io/) - Polkadot network statistics \(includes Kusama\). Shows

  network information and staking details from validators and intentions.

  [Github Repository](https://github.com/Colm3na/polkastats-v2/).

* [Panic](https://github.com/SimplyVC/panic_polkadot) - a node monitoring and alerting server for

  validators.

* [OpenWeb3/Guardian](https://github.com/open-web3-stack/guardian) - a CLI tool & JS library to

  monitor on chian states and events.

## Clients

* [Polkadot](https://github.com/paritytech/polkadot) - Rust implementation of the Polkadot Host.
* [Kagome](https://github.com/soramitsu/kagome) - A C++ Polkadot client developed by

  [Soramitsu](https://github.com/soramitsu).

* [Gossamer](https://github.com/ChainSafe/gossamer) - A Go implementation of the Polkadot Host.
* [Polkadot-JS client](https://github.com/polkadot-js/client) - Alternative client for JavaScript

  enthusiasts.

* [TX Wrapper](https://github.com/paritytech/txwrapper) - Helper funtions for offline transaction

  generation.

## Tools

* [Substrate](https://github.com/paritytech/substrate) - Blockchain development platform written in

  Rust. Polkadot is being built on top of Substrate.

* [Substrate Knowledge Base](https://substrate.dev/docs/en/) - Comprehensive documentation and

  tutorials for building a blockchain using Substrate.

* [Substrate VSCode plugin](https://github.com/paritytech/vscode-substrate).
* [Substrate Debug Kit](https://github.com/paritytech/substrate-debug-kit) - A collection of debug

  tools and libraries around substrate chains. Includes tools to calculate NPoS elections offline,

  disk usage monitoring, test templates against chain state and other pallet-specific helper.

* [Diener](https://crates.io/crates/diener) - a tool for easy changing of Polkadot or Substrate

  dependency versions.

* [Polkadot Launch](https://github.com/shawntabrizi/polkadot-launch) - a tool to easily launch

  custom local parachain-enabled Polkadot versions.

* [Halva](https://github.com/halva-suite/halva) - a Truffle-inspired local development environment

  for Substrate.

* [Fork-off Substrate](https://github.com/maxsam4/fork-off-substrate) - copies the state of an

  existing chain into your local version and lets you further experiment on it.

* [srtool](https://www.chevdor.com/tags/srtool/) - a tool for verifying runtime versions against

  on-chain proposal hashes.

* [sub-bench](https://github.com/nikvolf/sub-bench) - a tool to spam your node with transactions for

  the sake of benchmarking.

* [substrate-devhub-utils](https://github.com/danforbes/substrate-devhub-utils) - a set of

  JavaScript utilities making life with Substrate a little easier.

## UI

* [Polkadash](https://github.com/Swader/polkadash) - VueJS-based starter kit for custom user

  interfaces for Substrate chains. [Tutorials](https://dotleap.com/tag/tutorial/).

* [Polkadot JS Apps UI](https://github.com/polkadot-js/apps) - Repository of the

  [polkadot.js.org/apps](https://polkadot.js.org/apps) UI.

* [Substrate Front-end Template](https://github.com/substrate-developer-hub/substrate-front-end-template) -

  ReactJS-based starter UI for custom user interfaces for Substrate chains.

* [Polkadot JS Browser Extension](https://github.com/polkadot-js/extension) - key management in a

  Chrome extension.

## Libraries

### Polkadot-JS Common

Polkadot-JS Common provides various utility functions that are used across all projects in the `@polkadot` namespace and is split into a number of internal utility packages. The documentation and usage instructions are provided at [Polkadot-JS/Common API Documentation](https://polkadot.js.org/common/).

* [@polkadot/keyring](https://polkadot.js.org/common/keyring/) To create / load accounts in

  JavaScript, helpful for creating wallets or any application that will require the user to write to

  chain. [Examples](https://polkadot.js.org/docs/keyring/start/create).

* [@polkadot/util](https://polkadot.js.org/common/util/) Utility functions like checking if a string

  is hex-encoded.

* [@polkadot/util-crypto](https://polkadot.js.org/common/util-crypto/) Crypto utilities that will

  come in handy while developing with Polkadot.

### CLI Tools

* [@polkadot/api-cli](https://github.com/polkadot-js/tools/tree/master/packages/api-cli) Command

  line interface for the polkadot API. [Documentation](https://polkadot.js.org/docs/api/start).

* [@polkadot/monitor-rpc](https://github.com/polkadot-js/tools/tree/master/packages/monitor-rpc) RPC

  monitor for Polkadot. See the RPC tools below for additional information.

* [@polkadot/signer-cli](https://github.com/polkadot-js/tools/tree/master/packages/signer-cli) Tool

  to construct, sign, and broadcast transactions. Signing can be done offline.

* [Polkadot API Cpp](https://github.com/usetech-llc/polkadot_api_cpp) - С++ API for Polkadot, can

  build `clip`, a command line tool.

### WASM

Webassembly related tools and projects.

* [ink!](https://github.com/paritytech/ink/) - an eDSL to write WebAssembly based smart contracts

  using the Rust programming language.

* [parity-wasm](https://github.com/paritytech/parity-wasm) - Low-level WebAssembly format library.
* [wasm-utils](https://github.com/paritytech/wasm-utils) - Collection of WASM utilities used in

  pwasm-ethereum and substrate contract development.

* [wasmi](https://github.com/paritytech/wasmi) - a Wasm interpreter conceived as a component of

  parity-ethereum \(ethereum-like contracts in wasm\) and substrate.

### RPC and API Tools

* [@polkadot/api/rpc-provider](https://github.com/polkadot-js/api/tree/master/packages/rpc-provider)

  Demonstrates how the JS tools interact with the node over RPC.

* [RPC documentation](https://polkadot.js.org/docs/substrate/rpc).
* [Polkadot API Server by SimplyVC](https://github.com/SimplyVC/polkadot_api_server).
* [Go: Subscan API](https://github.com/itering/substrate-api-rpc).
* [C++ Polkadot API](https://github.com/usetech-llc/polkadot_api_cpp) - С++ API for Polkadot.
* [.NET Polkadot API](https://github.com/usetech-llc/polkadot_api_dotnet) - Polkadot Substrate API

  for .NET.

* [Python Polkadot API](https://github.com/polkascan/py-substrate-interface).
* [GSRPC](https://github.com/centrifuge/go-substrate-rpc-client/) - Substrate RPC client in Go,

  a.k.a. GSRPC.

* [Substrate API Sidecar](https://github.com/paritytech/substrate-api-sidecar) - an HTTP wrapper for

  Substrate, abstracting some complex RPC calls into simple REST calls.

* [Subxt](https://github.com/paritytech/substrate-subxt) - a Rust library to submit extrinsics to a

  Substrate node via RPC.

### SCALE Codec

The [SCALE](https://substrate.dev/docs/en/knowledgebase/advanced/codec) \(Simple Concatenated Aggregate Little-Endian\) Codec is a lightweight, efficient, binary serialization and deserialization codec.

It is designed for high-performance, copy-free encoding and decoding of data in resource-constrained execution contexts, like the Substrate runtime. It is not self-describing in any way and assumes the decoding context has all type knowledge about the encoded data.

It is used in almost all communication to/from Substrate nodes, so implementations in different languages exist:

* [Ruby](https://github.com/itering/scale.rb)
* [Rust](https://github.com/paritytech/parity-scale-codec)
* [Go](https://github.com/itering/scale.go)
* [C++](https://github.com/soramitsu/kagome/tree/master/core/scale)
* [TypeScript](https://github.com/polkadot-js/api)
* [AssemblyScript](https://github.com/LimeChain/as-scale-codec)
* [Haskell](https://github.com/airalab/hs-web3/tree/master/src/Codec)
* [Java](https://github.com/emeraldpay/polkaj)
* [Python](https://github.com/polkascan/py-scale-codec)

## Data Crawling and Conversion

The following tools help you extract and structure data from a Substrate node.

* [Polkascan PRE Harvester](https://github.com/polkascan/polkascan-pre-harvester)

  \([matching explorer for harvested data](https://github.com/polkascan/polkascan-pre-explorer-gui)\).

* [Parity's Substrate Archive](https://github.com/paritytech/substrate-archive).
* [Hydra: GraphQL Builder](https://github.com/Joystream/joystream).
* [Polka-store](https://github.com/TheGoldenEye/polka-store) - a tool which scans a Substrate chain

  and stores balance-relevant transactions in an SQLite database.

* [Substrate-graph](https://github.com/playzero/substrate-graph) - A compact indexer for Substrate based nodes providing a GraphQL interface.

  **Miscellaneous**

* [GSRPC: Substrate RPC Client in Go](https://github.com/centrifuge/go-substrate-rpc-client)
* [Chronologic Transaction Scheduler](https://blog.chronologic.network/how-to-schedule-edgeware-edg-transactions-ed4bae4c5648)
* [Edgeware Secure Mnemonic Phrase Generator for Lockdrop](https://github.com/luboremo/Edgeware-seed-generating-script-SSSS)

