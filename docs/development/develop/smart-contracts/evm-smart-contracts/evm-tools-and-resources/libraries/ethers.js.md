# Ethers.js

### Introduction <a href="introduction" id="introduction"></a>

The [ethers.js](https://docs.ethers.io) library provides a set of tools to interact with Ethereum Nodes with JavaScript, similar to web3.js. Edgeare has an Ethereum-like API available that is fully compatible with Ethereum-style JSON RPC invocations. Therefore, developers can leverage this compatibility and use the ethers.js library to interact with an Edgeware node as if they were doing so on Ethereum. You can read more about ethers.js on this [blog post](https://medium.com/l4-media/announcing-ethers-js-a-web3-alternative-6f134fdd06f3).

### Setup Ethers.js with Edgeware <a href="setup-ethersjs-with-moonbeam" id="setup-ethersjs-with-moonbeam"></a>

To get started with the ethers.js library, install it using the following command:

```
npm install ethers
```

Once done, the simplest setup to start using the library and its methods is the following:

```
const ethers = require('ethers');

// Variables definition
const privKey = '0xPRIVKEY';

// Define Provider
const provider = new ethers.providers.StaticJsonRpcProvider('RPC_URL', {
    chainId: ChainId,
    name: 'NETWORK_NAME'
});

// Create Wallet
let wallet = new ethers.Wallet(privKey, provider);
```

Different methods are available inside `provider` and `wallet`. Depending on which network you want to connect to, you can set the `RPC_URL, ChainID, NETWORK_NAME`to the following values:

**Edgeware development node:**

* RPC_URL:  [`http://localhost:9933/`](http://localhost:9933)``
* ChainId: `2021`
* NETWORK_NAME: `dev`

**Beresheet testnet:**

* RPC_URL:  [`https://beresheet2.edgewa.re/evm`](https://beresheet2.edgewa.re/evm)`(Alternatively, one can use `[`https://beresheetX.edgewa.re/evm`](https://beresheetx.edgewa.re/evm)` where X can be any number from 1 to 8.)`
* ChainId: `2022`
* NETWORK_NAME: `Beresheet`

**Edgeware mainnet:**

* RPC_URL: [`https://mainnet2.edgewa.re/evm`](https://mainnet2.edgewa.re/evm)`  (Alternatively, one can use  `[`https://mainnetX.edgewa.re/evm`](https://mainnetx.edgewa.re/evm)` where X can be any number from 1 to 20.)`
* Chain ID: `2021`
* NETWORK_NAME: `Edgeware`

### Tutorial for using Ethers.js on Edgeware

{% content-ref url="../../tutorials/deploy-an-evm-contract/using-ethers.js.md" %}
[using-ethers.js.md](../../tutorials/deploy-an-evm-contract/using-ethers.js.md)
{% endcontent-ref %}

