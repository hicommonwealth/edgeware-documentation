# Using Ethers.js

{% hint style="warning" %}
This is currently a resource page -- \('Walkthrough' in progress\).
{% endhint %}

### Introduction <a id="introduction"></a>

The [ethers.js](https://docs.ethers.io/) library provides a set of tools to interact with Ethereum Nodes with JavaScript, similar to web3.js. Edgeare has an Ethereum-like API available that is fully compatible with Ethereum-style JSON RPC invocations. Therefore, developers can leverage this compatibility and use the ethers.js library to interact with an Edgeware node as if they were doing so on Ethereum. You can read more about ethers.js on this [blog post](https://medium.com/l4-media/announcing-ethers-js-a-web3-alternative-6f134fdd06f3).

### Setup Ethers.js with Edgeware <a id="setup-ethersjs-with-moonbeam"></a>

To get started with the ethers.js library, install it using the following command:

```text
npm install ethers
```

Once done, the simplest setup to start using the library and its methods is the following:

```text
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

* RPC\_URL:  [`http://localhost:9933/`](http://localhost:9933/)\`\`
* ChainId: `2021`
* NETWORK\_NAME: `dev`

**Beresheet testnet:**

* RPC\_URL:  [`https://beresheet2.edgewa.re/evm`](https://beresheet2.edgewa.re/evm)`(Alternatively, one can use` [`https://beresheetX.edgewa.re/evm`](https://beresheetX.edgewa.re/evm) `where X can be any number from 1 to 8.)`
* ChainId: `2022`
* NETWORK\_NAME: `Beresheet`

**Edgeware mainnet:**

* RPC\_URL: [`https://mainnet2.edgewa.re/evm`](https://mainnet2.edgewa.re/evm) `(Alternatively, one can use` [`https://mainnetX.edgewa.re/evm`](https://mainnetX.edgewa.re/evm) `where X can be any number from 1 to 20.)`
* Chain ID: `2021`
* NETWORK\_NAME: `Edgeware`

