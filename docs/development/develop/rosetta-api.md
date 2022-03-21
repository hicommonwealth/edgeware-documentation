# Rosetta API

## [https://github.com/edgeware-network/substrate-rosetta-api](https://github.com/edgeware-network/substrate-rosetta-api)

## Introduction

[Rosetta API](https://www.rosetta-api.org/) is a development tool built by [Coinbase](https://coinbase.com/) that allows blockchains to be more readily compatible with a variety of third-party software, including exchanges (like Coinbase,) wallets, OTC desks, and applications.

In combination with [Substrate,](https://substrate.dev/) which is a [flexible,](https://substrate.io/technology/flexible/) [open,](https://substrate.io/technology/open/) [interoperable,](https://substrate.io/technology/interoperable/) and [future-proof](https://substrate.io/technology/future-proof/) framework for developing blockchains, we have two industry-leading ways of developing and interoperating with blockchain-based platforms. The benefits of this combination allow any Substrate chain to trivially implement compatible tools, such as this repository of Rosetta API.

## Prerequisites

**Archive Node Access**

You will need access to an **[archive node](https://wiki.polkadot.network/docs/maintain-sync)** [](https://wiki.polkadot.network/docs/maintain-sync) to be able to query the whole blockchain. You may use publicly available nodes or you can run one locally using the `--pruning archive`flag when you start the node. You can also use the `--wasm-execution Compiled` flag to speed up synchronization time significantly however, this uses more CPU and RAM, so you should turn it off after sync is complete.

**Setting up Rosetta-api**

1.  `git clone https://github.com/edgeware-network/substrate-rosetta-api`
2.  Edit configuration files appropriately for your chain. These are located in the `networks` folder. The information can be found in the node itself and on [subscan](https://polkadot.subscan.io/) or your preferred block explorer. You can also use [Polkadot apps.](https://polkadot.js.org/apps/#/explorer)
3.  Add your chains metadata in hexadecimal format in `networks/metadata` . You can get this by using [subxt CLI tool](https://github.com/paritytech/subxt) it defaults to a node running locally or you can use a different node by indicating the --url.
    -  1.  You can get the metadata by running the command `subxt metadata --format hex`
4.  Add your chains types. This can be done in one of two ways:
    -  1.  Add the types manually into the `polkadot-types.json` file.
        2.  If your chain uses a node package like Edgeware you add your chain spec to `src/helpers/connections.js` with types in `class SubstrateNetworkConnection`
5.  Once those are completed run `yarn install` and `yarn start`.
    

**Setting up Rosetta-cli**

1.  In a separate terminal test with [rosetta-cli](https://github.com/coinbase/rosetta-cli ) Once downloaded you will most likely have to set your path for rosetta-cli using this command `export PATH=$PATH:/Users/bin` for example.

3.  Once that is set `Use "rosetta-cli [command] --help" for more information about a command.` This is a list of rosetta-cli command examples. Notice that you have to indicate what configuration file you want to us every time.

5.  `rosetta-cli view:balance '{"address":"ADDRESS-GOES-HERE"}' BLOCK-NUMBER-GOES-HERE --configuration-file ./rosetta-api/rosetta-cli/mainnet/config.json`

7.  `rosetta-cli view:block BLOCK-NUMBER-GOES-HERE --configuration-file ./Depth-rosetta-api/rosetta-cli/mainnet/config.json`

9.  `rosetta-cli view:networks --configuration-file ./rosetta-api/rosetta-cli/mainnet/config.json`

11.  `rosetta-cli check:data --configuration-file ./rosetta-api/rosetta-cli/mainnet/config.json`

Try all possible tests with rosetta-cli.

-   Now you have a working instance of rosetta-api for your substrate chain. Please feel free to let us know how we can improve it in the future. Our api is your API.

## Contact us:

Discord: [https://discord.gg/wFbystdrHC](https://discord.gg/wFbystdrHC)

Telegram: [https://t.me/heyedgeware](https://t.me/heyedgeware)

## Further Resources:

1.  [https://www.rosetta-api.org/](https://www.rosetta-api.org/)
2.  [https://www.rosetta-api.org/docs/welcome.html](https://www.rosetta-api.org/docs/welcome.html)
3.  [https://community.rosetta-api.org/](https://community.rosetta-api.org/)
4.  [https://docs.substrate.io/](https://docs.substrate.io/)
5.  [https://polkadot.js.org/apps/#/explorer](https://polkadot.js.org/apps/#/explorer)
6.  [https://www.subscan.io/](https://www.subscan.io/)