# Using Remix - Ethereum IDE

<h2>Introduction</h2>

This guide walks through the process of creating and deploying a Solidity-based smart contract to a Edgeware dev node using the [Remix IDE](https://remix.ethereum.org/). Remix is one of the commonly used development environments for smart contracts on Ethereum. Given Edgeware’s Ethereum compatibility features, Remix can be used directly with a Edgeware node.

This guide assumes that you have a running local Edgeware node running in `--dev mode`, and that you have a MetaMask installation configured to use this local node. [You can find instructions for running a local Edgeware EVM node](https://contracts.edgewa.re/#/4/setting-up-a-local-node) and to [configure MetaMask for Edgeware](https://contracts.edgewa.re/#/4/interacting-with-a-Edgeware-node-using-metamask).

<h2>Interacting With Edgeware Using Remix</h2>

[Open Remix](https://remix.ethereum.org/) and click on the `New File`

<img width="1647"  src="https://user-images.githubusercontent.com/32852637/111375571-c850d100-8674-11eb-933a-a8f848f0cdac.png">

Name your file, in our case we've named it `erc20.sol` - yes, that [famous token standard](https://eips.ethereum.org/EIPS/eip-20)

<img width="1647"  src="https://user-images.githubusercontent.com/32852637/111375649-e74f6300-8674-11eb-956e-5a5c2acf8495.png">

Now add code. Here we are using simple ERC-20 contract based on the current Open Zeppelin ERC-20 template. It creates `MyFirstToken` with symbol `HEDGE` and mints the entirety of the initial supply to the creator of the contract.

```
pragma solidity ^0.6.0;

import 'https://github.com/OpenZeppelin/openzeppelin-contracts/blob/release-v3.1.0/contracts/token/ERC20/ERC20.sol';

// This ERC-20 contract mints the specified amount of tokens to the contract creator.
contract MyFirstToken is ERC20 {
  constructor(uint256 initialSupply) ERC20("MyFirstToken", "HEDGE") public {
    _mint(msg.sender, initialSupply);
  }
}
```
<img width="1647"  src="https://user-images.githubusercontent.com/32852637/111376053-5fb62400-8675-11eb-9fb0-8b5235f5f47f.png">

On the left sidebar, you will click on Solidity compiler and Compile erc20.sol

```
Solidity Compiler >>> Compile Contract

```
<img width="1411"  src="https://user-images.githubusercontent.com/32852637/111376159-78bed500-8675-11eb-8a39-d9a6e7ca8def.png">

Now click to the `Deploy & Run Transactions` on the left in the sidebar and open Metamask to check if is our account connected. If it's connected you can skip to next steps

<img width="1411"  src="https://user-images.githubusercontent.com/32852637/111376794-4b265b80-8676-11eb-9ac7-f33e65bf6942.png">

Select our account, in this case it's `Account 4` and click on connect

<img width="1411"  src="https://user-images.githubusercontent.com/32852637/111376854-5d07fe80-8676-11eb-9b0f-5733d70ed360.png">

You will now head to deploy contract. Just before that, make sure you've set set **ENVIRONMENT** to `Injected Web3` and Account that we've imported. Hint, it should have some Eth. To the input next deploy input `initialSupply`, in our case it's 21M. Since this contract uses the default of 18 decimals, the value you will put there is `21000000000000000000000000`

<img width="1411"  src="https://user-images.githubusercontent.com/32852637/111376936-790ba000-8676-11eb-8674-3edf868358aa.png">

You will hit **confirm!**

<img width="1295"  src="https://user-images.githubusercontent.com/32852637/111377010-8d4f9d00-8676-11eb-8cf8-a9d73d210b4c.png">

You will see your contract has been successfully deployed.

<img width="1411"  src="https://user-images.githubusercontent.com/32852637/111377050-99d3f580-8676-11eb-94e1-b40111463dbb.png">

You can see your contract deployment details, that has been successfully deployed on Edgeware EVM.

<img width="1411"  src="https://user-images.githubusercontent.com/32852637/111377094-a6f0e480-8676-11eb-915e-47e0a29d7369.png">

You can now click to call functions like `decimals`, `name`, `symbol`, `totalSupply`

<img width="1411" alt="UsingRemix11" src="https://user-images.githubusercontent.com/32852637/111377216-c38d1c80-8676-11eb-8b29-aaa634bbbabc.png">

<h2>What's next?</h2>

You can copy your contracts address and add it to Metamask to play out! Have fun, stay safe!

<h2>Reach us for more engagement</h2>

Glad you've made it through! 🥰 We are eager to guide your more on your exploration through Edgeware Ethereum compability feature. We are **keen to hear your experience and suggestions you may have for us..** You can feel free to [chat with us in the Edgeware's channels like Discord, Element and Telegram](https://linktr.ee/edg_developers), we can help you out with issues you may have or project you may want to be funded through our [Treasury program](https://docs.edgewa.re/edgeware-runtime/treasury). Don't hesitate to share your feedback on our channels, there is always space to improve! 🙌





























