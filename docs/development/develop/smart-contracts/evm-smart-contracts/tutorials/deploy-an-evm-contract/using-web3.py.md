# Using Web3.py

{% hint style="warning" %}
This is currently a resource page -- \('Walkthrough' in progress\).
{% endhint %}

### Introduction <a id="introduction"></a>

[Web3.py](https://web3py.readthedocs.io/) is a set of libraries that allow developers to interact with Ethereum nodes using HTTP, IPC, or WebSocket protocols with Python. Moonbeam has an Ethereum-like API available that is fully compatible with Ethereum-style JSON RPC invocations. Therefore, developers can leverage this compatibility and use the web3.py library to interact with a Moonbeam node as if they were doing so on Ethereum.

### Setup Web3.py with Edgeware <a id="setup-web3py-with-moonbeam"></a>

To get started with the web3.py library, install it using the following command:

```text
pip3 install web3
```

Once done, the simplest setup to start using the library and its methods is the following:

```text
from web3 import Web3

web3 = Web3(Web3.HTTPProvider('RPC_URL'))
```

Depending on which network you want to connect to, you can set the `RPC_URL` to the following values:

**Edgeware development node:**

* RPC\_URL:  [`http://localhost:9933/`](http://localhost:9933/)\`\`

**Beresheet testnet:**

* RPC\_URL:  [`https://beresheet2.edgewa.re/evm`](https://beresheet2.edgewa.re/evm)`(Alternatively, one can use` [`https://beresheetX.edgewa.re/evm`](https://beresheetX.edgewa.re/evm) `where X can be any number from 1 to 8.)`

**Edgeware mainnet:**

* RPC\_URL: [`https://mainnet2.edgewa.re/evm`](https://mainnet2.edgewa.re/evm) `(Alternatively, one can use` [`https://mainnetX.edgewa.re/evm`](https://mainnetX.edgewa.re/evm) `where X can be any number from 1 to 20.)`



