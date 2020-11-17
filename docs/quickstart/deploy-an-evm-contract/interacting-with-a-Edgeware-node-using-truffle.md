# Interacting with Edgeware EVM using Truffle

### Introduction

This guide walks through the process of deploying a Solidity-based smart contract to a Edgeware node using [Truffle](https://www.trufflesuite.com/docs). [Truffle](https://www.trufflesuite.com/docs) is one of the commonly used development tools for smart contracts on Ethereum. Given Edgeware's Ethereum compatibility features, Truffle can be used directly with a Edgeware node.

This guide assumes that you have a [running local Edgeware EVM node running in `--dev` mode.](4/setting-up-a-local-node.md). 

### Environment Prerequisites

Installed [Nodejs](https://nodejs.org/en/) and particular package manager like [yarn](https://classic.yarnpkg.com/en/docs/install/#mac-stable) or [npm](https://www.npmjs.com/get-npm), rest we have batteries included in this tutorial. 
When you are ready, clone our tutorial repository with prepared stack for you

```shell
git clone https://github.com/edgeware-builders/tutorials tutorials;cd tutorials/truffle;yarn

```
It will move to your cloned repository, install required packages and you are ready to go!

Let's take sneak peak to `truffle-config.js` in `truffle/` directory

```javascript
const EdgewarePrivateKeyProvider = require('./private-provider')

var edgewarePrivateKey = "99B3C12287537E38C90A9219D4CB074A89A16E9CDB20BF85728EBD97C343E342";

module.exports = {
  compilers: {
    solc: {
      version: "^0.6.0",
    }
  },
  networks: {
    development: {
      provider: () => new EdgewarePrivateKeyProvider(edgewarePrivateKey, "http://localhost:9933/", 42),
      network_id: 42,
      skipDryRun: true,
      gasPrice: 1000000000
    },
  } 
}
```
You notice few facts from here, our chainId is `42` and we are using solc version above `^0.6.0`.

> **Note** We are using a `PrivateKeyProvider` as our Web3 provider (instantiation included in `private-provider.js`). This provider is being set up in a very specific way to work around some issues we are currently working on related to `chainid`, `nonce handling`, and the `skipCache: true` setting when using the default Truffle-provided Web3 provider with Edgeware EVM nodes. We also are using the same private key that we have been using in other guides, which comes pre-funded with tokens `tEDG` via the genesis config of a Edgeware EVM node running in `--dev` mode. The public key for this account is: `0x6Be02d1d3665660d22FF9624b7BE0551ee1Ac91b`.

The contract we will be deploying with Truffle is a simple ERC-20 contract. Youn can find this contract under `truffle/contracts/HedgeToken.sol`, it's content is showed here

### ERC-20 Contract 

```javascript
// SPDX-License-Identifier: MIT
pragma solidity ^0.6.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract HedgeToken is ERC20 {
    constructor(uint256 initialSupply) public ERC20("HedgeToken", "HEDGE") {
        _mint(msg.sender, initialSupply);
    }
}
```

It's Simple ERC-20 contracted based on the OpenZepplin ERC20 contract that creates `HedgeToken` and assigns the created initial token supply to the contract creator.

You can notice initial supply in `migrations/2_deploy.contracts.js`, it contains the following:

```javascript
var HedgeToken = artifacts.require("HedgeToken");

module.exports = function (deployer) {
  deployer.deploy(HedgeToken, "21000000000000000000000000", { gas: 2100000000 });
};
```

`21000000000000000000000000` is the number of tokens to initially mint with the contract, that is 21 Milion with 18 decimal places. [Since OpenZepplin v3.0+, there is default decimal 18 for SimpleToken.sol](https://docs.openzeppelin.com/contracts/3.x/api/token/erc20#ERC20-_setupDecimals-uint8-)

Now let's go to the essential part! After you had installed neccesary packages, continue in terminal with following command

### Compile ERC-20 Contract
```
npx truffle compile
```
![truffle-compile](assets/truffle-compile.png)

What id does, it take OpenZepplin ERC20.sol token, compiles it with other referenced code in other OpenZepplin code, creates artifact (bytecode) and ABI (contract interface)

### Deploying a Contract to Edgeware EVM Using Truffle

Now let's go to the hot stuff, deploy it to our Edgeware EVM

```
npx truffle --network development migrate
```
![truffle-migrate](assets/truffle-migrate.png)

As you may see, we are using our `development` network from `truffle-config.js`. From migrate you'll notice there whats our contract address of our contract.

### Reach us for more engagement

Glad you've made it through! 🥰 We are eager to guide your more on your exploration through Edgeware Ethereum compability feature. We are **keen to hear your experience and suggestion you may for us.**. You can feel free to [chat with us in the Edgeware's channels like Discord, Element and Telegram](https://linktr.ee/edg_developers), we can help you out with issues you may have or project you may want to be funded through our [Treasury program](https://docs.edgewa.re/edgeware-runtime/treasury). Don't hesitate to share your feedback on our channels, there is always space to improve! 🙌
