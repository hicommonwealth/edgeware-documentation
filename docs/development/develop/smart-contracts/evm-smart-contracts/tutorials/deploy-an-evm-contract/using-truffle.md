# Using Truffle

## Interacting with Edgeware EVM using Truffle <a id="interacting-with-edgeware-evm-using-truffle"></a>

### Introduction <a id="introduction"></a>

This guide walks through the process of deploying a Solidity-based smart contract to a Edgeware node using [Truffle](https://www.trufflesuite.com/docs). Truffle is one of the commonly used development tools for smart contracts on Ethereum. Given Edgeware's Ethereum compatibility features, Truffle can be used directly with a Edgeware node.

This guide assumes that you have a [running local Edgeware EVM node running in `--dev` mode.](https://main.edgeware.wiki/development/develop/smart-contracts/evm-smart-contracts/tutorials/deploy-an-evm-contract/setting-up-a-edgeware-evm-node).

### Environment Prerequisites <a id="environment-prerequisites"></a>

Installed [Nodejs](https://nodejs.org/en/) and particular package manager like [yarn](https://classic.yarnpkg.com/en/docs/install/#mac-stable) or [npm](https://www.npmjs.com/get-npm), rest we have batteries included in this tutorial. When you are ready, clone our tutorial repository with prepared stack for you

```bash
git clone https://github.com/edgeware-builders/tutorials tutorials;cd tutorials/truffle;yarn
```

It will move to your cloned repository, install required packages and you are ready to go!

Let's take sneak peak to `truffle-config.js` in `truffle/` directory

```rust
const HDWalletProvider = require("@truffle/hdwallet-provider");
const privKey = '1111111111111111111111111111111111111111111111111111111111111111';

module.exports = {
  compilers: {
    solc: {
      version: "^0.6.0",
    }
  },
  networks: {
    development: {
      provider: () => new HDWalletProvider({
        privateKeys: [ privKey ],
        providerOrUrl: "http://localhost:9933/",
      }),
      network_id: 2021,
    },
  } 
}
```

You notice few facts from here, our chainId is `2021` and we are using solc version above `^0.6.0`.

> **Note** We are using the same private key that we have been using in other guides, which comes pre-funded with tokens `tEDG` via the genesis config of a Edgeware EVM node running in `--dev` mode. The public key for this account is: `0x19e7e376e7c213b7e7e7e46cc70a5dd086daff2a`.

The contract we will be deploying with Truffle is a simple ERC-20 contract. You can find this contract under `truffle/contracts/HedgeToken.sol`, it's content is showed here

### \[ERC-20 Contract\]

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
  deployer.deploy(HedgeToken, "21000000000000000000000000");
};
```

`21000000000000000000000000` is the number of tokens to initially mint with the contract, that is 21 Million with 18 decimal places. [Since OpenZepplin v3.0+, there is default decimal 18 for SimpleToken.sol](https://docs.openzeppelin.com/contracts/3.x/api/token/erc20#ERC20-_setupDecimals-uint8-)

Now let's go to the essential part! After you had installed necessary packages, continue in terminal with following command

### Compile ERC-20 Contract <a id="compile-erc-20-contract"></a>

```text
npx truffle compile
```

![](https://user-images.githubusercontent.com/32852637/122429916-24bbd900-cf61-11eb-98bd-faa07d223e68.PNG)

What id does, it take OpenZepplin ERC20.sol token, compiles it with other referenced code in other OpenZepplin code, creates artifact \(bytecode\) and ABI \(contract interface\)

### Deploying a Contract to Edgeware EVM Using Truffle <a id="deploying-a-contract-to-edgeware-evm-using-truffle"></a>

Now let's go to the hot stuff, deploy it to our Edgeware EVM

```text
npx truffle --network development migrate
```

![Truffle\_2](https://user-images.githubusercontent.com/32852637/122431469-7ca70f80-cf62-11eb-8684-114f0323ff83.PNG)

As you may see, we are using our `development` network from `truffle-config.js`. From migrate you'll notice there what our contract address is of our contract.

### Reach us for more engagement <a id="reach-us-for-more-engagement"></a>

Glad you've made it through! 🥰 We are eager to guide your more on your exploration through Edgeware Ethereum combability feature. We are **keen to hear your experience and suggestions you may have for us.**. You can feel free to [chat with us in the Edgeware's channels like Discord, Element and Telegram](https://linktr.ee/edg_developers), we can help you out with issues you may have or project you may want to be funded through our <A HREF = "https://docs.edgeware.wiki/edgeware-stack/economics/treasury">Treasury program</A>. Don't hesitate to share your feedback on our channels, there is always space to improve! 🙌

