# Using Remix - Ethereum IDE

## Introduction <a id="introduction"></a>

This guide walks through the process of creating and deploying a Solidity-based smart contract to a Edgeware dev node using the [Remix IDE](https://remix.ethereum.org/). Remix is one of the commonly used development environments for smart contracts on Ethereum. Given Edgeware’s Ethereum compatibility features, Remix can be used directly with a Edgeware node.

This guide assumes that you have a running local Edgeware node running in `--dev` mode, and that you have a MetaMask installation configured to use this local node. <A HREF = "https://docs.edgeware.wiki/development/develop/smart-contracts/evm-smart-contracts/tutorials/deploy-an-evm-contract/setting-up-a-edgeware-evm-node">You can find instructions for running a local Edgeware EVM node</A> and to <A HREF = "https://main.edgeware.wiki/contribute-and-engage/develop/edgeware-smart-contracts/deploy-an-evm-contract/using-metamask">configure MetaMask for Edgeware</A>.

## Interacting With Edgeware Using Remix <a id="interacting-with-edgeware-using-remix"></a>

[Open Remix](https://remix.ethereum.org/) and click on the `New File`

Name your file, in our case we've named it `ERC20.sol` - yes, that [famous token standard](https://eips.ethereum.org/EIPS/eip-20)

![](https://user-images.githubusercontent.com/44712760/122647263-91a9ad00-d0e0-11eb-93fb-1516d5c70509.png)

Now add code. Here we are using simple ERC-20 contract based on the current Open Zeppelin ERC-20 template. It creates `MyFirstToken` with symbol `HEDGE` and mints the entirety of the initial supply to the creator of the contract.

```text
pragma solidity ^0.6.0;

import 'https://github.com/OpenZeppelin/openzeppelin-contracts/blob/release-v3.1.0/contracts/token/ERC20/ERC20.sol';

// This ERC-20 contract mints the specified amount of tokens to the contract creator.
contract MyFirstToken is ERC20 {
  constructor(uint256 initialSupply) ERC20("MyFirstToken", "HEDGE") public {
    _mint(msg.sender, initialSupply);
  }
}
```

![](https://user-images.githubusercontent.com/44712760/122647352-1eed0180-d0e1-11eb-83f2-652e5d071d28.png)

On the left sidebar, you will click on Solidity compiler and Compile ERC20.sol

```text
Solidity Compiler >>> Compile Contract
```

![](https://user-images.githubusercontent.com/44712760/122647422-683d5100-d0e1-11eb-8ec4-d987d7ed8365.png)

Now click to the `Deploy & Run Transactions` on the left in the sidebar and open Metamask to check if is our account connected. If it's connected you can skip to next steps

![](https://user-images.githubusercontent.com/44712760/122647516-cb2ee800-d0e1-11eb-91c8-78da242aca5b.png)

Select our account, in this case it's `Edgeware Dev` and click **connect** if you don't see that option click on **Not connected** a new window will pop up.

![](https://user-images.githubusercontent.com/44712760/122647653-8ce5f880-d0e2-11eb-8775-1c0a8040e6db.png) ![](https://user-images.githubusercontent.com/44712760/122647679-a71fd680-d0e2-11eb-890d-18a72131a25d.png)

You will now head to deploy contract. Just before that, make sure you've set set **ENVIRONMENT** to `Injected Web3` and Account that we've imported. Hint, it should have some Eth. To the input next deploy input `initialSupply`, in our case it's 21M. Since this contract uses the default of 18 decimals, the value you will put there is `21000000000000000000000000`

![](https://user-images.githubusercontent.com/44712760/122647765-0aaa0400-d0e3-11eb-8163-a3bf7778d3d0.png)

You will hit **confirm**!

![Remix-MM-confirm](https://user-images.githubusercontent.com/44712760/122647786-27ded280-d0e3-11eb-8e16-46ca0bda1982.png)

You will see your contract has been successfully deployed.

![Remix-deployed-contract](https://user-images.githubusercontent.com/44712760/122647859-886e0f80-d0e3-11eb-9b90-3da70fefe94a.png)

You can see your contract deployment details, that has been successfully deployed on Edgeware EVM

![](https://user-images.githubusercontent.com/44712760/122647914-db47c700-d0e3-11eb-98ad-747ff2befd04.png)

You can now click to call functions like `decimals`, `name`, `symbol`, `totalSupply`

![](https://user-images.githubusercontent.com/44712760/122647936-f61a3b80-d0e3-11eb-9657-ae4a4914dc4b.png)

## What's next? <a id="what39s-next"></a>

You can copy your contracts address and add it to Metamask to play out! Have fun, stay safe!

## Reach us for more engagement <a id="reach-us-for-more-engagement"></a>

Glad you've made it through! 🥰 We are eager to guide your more on your exploration through Edgeware Ethereum combability feature. We are **keen to hear your experience and suggestions you may have for us.**. You can feel free to [chat with us in the Edgeware's channels like Discord, Element and Telegram](https://linktr.ee/edg_developers), we can help you out with issues you may have or project you may want to be funded through our <A HREF = "https://docs.edgeware.wiki/edgeware-stack/economics/treasury">Treasury program</A>. Don't hesitate to share your feedback on our channels, there is always space to improve! 🙌

