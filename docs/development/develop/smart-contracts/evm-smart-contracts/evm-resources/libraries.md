# Ethereum Libraries

{% hint style="warning" %}
#### Proceed with caution! This page is under progress. 🏗 
{% endhint %}

In order for a web app to interact with the Ethereum blockchain \(i.e. read blockchain data and/or send transactions to the network\), it must connect to an Ethereum node.

For this purpose, every Ethereum client implements the [JSON-RPC](https://ethereum.org/en/developers/docs/apis/json-rpc/) specification, so there are a uniform set of [endpoints](https://ethereum.org/en/developers/docs/apis/json-rpc/endpoints/) that applications can rely on.

If you want to use JavaScript to connect with an Ethereum node, it's possible to use vanilla JavaScript but several convenience libraries exist within the ecosystem that make this much easier. With these libraries, developers can write intuitive, one-line methods to initialize JSON RPC requests \(under the hood\) that interact with Ethereum.

**Why use a library?**

These libraries abstract away much of the complexity of interacting directly with an Ethereum node. They also provide utility functions \(e.g. converting ETH to Gwei\) so as a developer you can spend less time dealing with the intricacies of Ethereum clients and more time focused on the unique functionality of your application.

For more information on [Ethereum libraries click here](https://ethereum.org/en/developers/docs/apis/javascript/)

### Using libraries with Edgeware

{% page-ref page="../tutorials/deploy-an-evm-contract/using-web3.md" %}

{% page-ref page="../tutorials/deploy-an-evm-contract/using-web3.py.md" %}

{% page-ref page="../tutorials/deploy-an-evm-contract/using-ethers.js.md" %}

### Official library documentation guides

{% embed url="https://web3js.readthedocs.io/en/v1.5.2/" caption="Official documentation - web3.js" %}

{% embed url="https://web3py.readthedocs.io/en/stable/" caption="Official documentation - web3.py" %}

{% embed url="https://docs.ethers.io/v5/" caption="Official documentation - ethers.js" %}



