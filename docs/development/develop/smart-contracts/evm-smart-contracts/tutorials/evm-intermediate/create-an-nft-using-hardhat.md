# Deploy an NFT on Edgeware using Hardhat

\
Guided tutorial on how to setup and deploy an [ERC721](https://ethereum.org/en/developers/docs/standards/tokens/erc-721/) Non-Fungible Token (NFT) to a local network, as well as Edgeware's testnet (Beresheet), and mainnet network(s) using the [Hardhat Ethereum development](https://hardhat.org).

![](../../../../../../../.gitbook/assets/0\_ijgax8s5e0mwu2gx.jpg)

### Setting up the project

Let’s start an npm project first:

```javascript
npm init --yes
```

Then install the Hardhat package:

```javascript
npm install --save-dev hardhat@2.2.1
```

Now you are ready to create a new Hardhat project:

```javascript
npx hardhat
```

Choose `Create an empty hardhat.config.js`

![](https://static.slab.com/prod/uploads/9yelyblh/posts/images/a-Rx_k90pwNScSCoH0olMsvj.png)

This will create `hardhat.config.js` in your root directory with the solidity compiler version specified:

```javascript
/**
 * @type import('Hardhat/config').HardhatUserConfig
 */
module.exports = {
  solidity: "0.7.3",};
```

{% tabs %}
{% tab title="Potential Error" %}
{% hint style="danger" %}
 Error: 'You need to install hardhat locally to use it.' 
{% endhint %}
{% endtab %}

{% tab title="Solution" %}
{% hint style="success" %}
Run: **`npm install -save-dev "hardhat@^2.6.5"`** in your hardhat project's root directory
{% endhint %}
{% endtab %}
{% endtabs %}

### How to Write and Compile the Contract

We will start by writing a simple contract and then we'll compile it.

{% tabs %}
{% tab title="terminal" %}
```javascript
 mkdir contracts && cd contracts && touch MyEdgNFT.sol
```
{% endtab %}
{% endtabs %}

We'll use the open-zeppelin package to write our NFT contract. So first, install the open-zeppelin package:

{% tabs %}
{% tab title="terminal" %}
```javascript
npm install --save-dev @openzeppelin/contracts@3.4.0
```
{% endtab %}
{% endtabs %}

Here is the contract code we will be compiling:

{% tabs %}
{% tab title="MyEdgNFT.sol" %}
```javascript
pragma solidity ^0.7.3;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";

contract MyEdgNFT is ERC721 {
    constructor(string memory name, string memory symbol)
        ERC721(name, symbol)
    {}
}
```
{% endtab %}
{% endtabs %}

The first thing you need to do in any solidity file is to declare the compiler version. Then we can import the ERC721 contract (NFT contract) from open-zeppelin just like you do in JavaScript.

Solidity is a contract-oriented language. Just like an object-oriented language, contracts can have members such as functions and variables. In our code, we have only the constructor, which will be called when we deploy our contract.

Our contract inherits the ERC721 and then passes the `name` and `symbol` arguments which are going to be passed to the ERC721 contract. They literally decide the name and symbol of your NFT token.

We will pass whatever values we want to `name` and `symbol` at the point of deployment.

To compile it, run:

```javascript
npx hardhat compile
```

You might get some warnings but we'll ignore them to keep things simple. You should see `Compilation finished successfully` at the bottom.

You should also notice that the `/arfifacts` and `/cache` directories were generated. You don’t have to worry about them for this post, but it’s good to keep in mind that you can use `abi` in the artifacts if you want to interact with the contract when you build the frontend.

### How to Test the Contract

Since smart contracts are mostly financial applications – and they're also hard to change – testing is critical.

We will use some packages for testing. Install with the command below:

```javascript
npm install --save-dev @nomiclabs/hardhat-waffle ethereum-waffle chai @nomiclabs/hardhat-ethers ethers
```

`ethereum-waffle` is a testing framework for smart contracts. `chai` is an assertion library. We'll write tests in waffle using Mocha alongside Chai. `ethers.js` is a JavaScript SDK for interacting with the Ethereum blockchain. The other two packages are plugins for Hardhat.

Now, let’s make a new directory `test` in the root directory and make a new file called `test.js` in it:

```javascript
mkdir test && cd test && touch test.js
```

Make sure you require `@nomiclabs/hardhat-ethers` in the `hardhat.config.js` to make it available everywhere:

```javascript
require("@nomiclabs/hardhat-ethers");
```

Here is a simple test:

{% tabs %}
{% tab title="test.js" %}
```javascript
const { expect } = require("chai");

describe("MyEdgNFT", function () {
  it("Should return the right name and symbol", async function () {
    const MyEdgNFT = await hre.ethers.getContractFactory("MyEdgNFT");
    const myEdgNFT = await MyEdgNFT.deploy("MyEdgNFT", "ENFT");

    await myEdgNFT.deployed();
    expect(await myEdgNFT.name()).to.equal("MyEdgNFT");
    expect(await myEdgNFT.symbol()).to.equal("ENFT");
  });
});
```
{% endtab %}
{% endtabs %}

This code deploys our contract to the local Hardhat network and then checks if the `name` and `symbol` values are what we expect.

Run the test:

![](https://static.slab.com/prod/uploads/9yelyblh/posts/images/4ZJr8Bm04qpaG41lilrJLiTl.png)

Awesome, it passed the test!

#### How to Use console.log() in Hardhat

Now here is the coolest thing you can do with Hardhat. You can use `console.log()` just like you do in JavaScript, which was not possible before. `console.log()` alone is more than enough reason to switch to Hardhat.

Let’s go back to your solidity file and use `console.log()`.

{% tabs %}
{% tab title="" %}
```javascript
pragma solidity ^0.7.3;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";
import "hardhat/console.sol";

contract MyEdgNFT is ERC721 {
    constructor(string memory name, string memory symbol) ERC721(name, symbol) {
        console.log("name", name);
        console.log("symbol", symbol);
        console.log("msg.sender", msg.sender); //msg.sender is the address that initially deploys a contract
    }
}
```
{% endtab %}
{% endtabs %}

And run the test again with `npx hardhat test`. Then the command will compile the contract again, and then run the test. You should be able to see some values logged from the contract.

![](https://static.slab.com/prod/uploads/9yelyblh/posts/images/C4NJZKKP1XRcniUmaTM85Z1m.png)

This makes debugging a lot easier for you.

One caveat is that it supports only these data types:

* uint
* string
* bool
* address

But other than that, you can use it as if you are writing JavaScript.

### How to Deploy the Contract

All right! Now let’s deploy our contract. We can deploy our contract to one of the testing networks, the Mainnet, or even a mirrored version of the Mainnet in local.

We'll give a walkthrough here on how to deploy to your local machine.

Make a new directory called `scripts` in the root directory and `deploy.js` in it.

{% tabs %}
{% tab title="terminal" %}
```javascript
mkdir scripts && cd scripts && touch deploy.js
```
{% endtab %}
{% endtabs %}

Here is the deploy script. You deploy along with constructor values:

{% tabs %}
{% tab title="deploy.js" %}
```javascript
async function main()  {
const MyEdgNFT = await hre.ethers.getContractFactory("MyEdgNFT");
const myEdgNFT = await MyEdgNFT.deploy("MyEdgNFT", "ENFT");
await myEdgNFT.deployed();
console.log("MyEdgNFT deployed to:", myEdgNFT.address);
}
main()
.then(() => process.exit(0))
.catch((error) => {
    console.error(error);
    process.exit(1);
});
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
You might want to remove `console.log()` before you deploy. And then run this deploy script with:
{% endhint %}

{% tabs %}
{% tab title="terminal" %}
```javascript
npx hardhat run scripts/deploy.js
```
{% endtab %}
{% endtabs %}

Boom! Now your NFT contract is deployed to the local network.

![](https://static.slab.com/prod/uploads/9yelyblh/posts/images/ylQ7Iz4lIlXwvjefoUBsRn9T.png)

You can target any network configured in the `hardhat.config.js` depending on your needs. You can find more about configuration [here](https://hardhat.org/config/).

## Hardhat Configuration File

We need to modify our Hardhat configuration file so we can compile and deploy contracts into the Edgeware ecosystem. If you have not yet done so, connect your MetaMask Account to our ecosystem and fund it with the [automated faucet bot on discord](https://discord.gg/yBDq3FJat9). We will use the private key of the account created to deploy the contract. If you don’t know the private key, you can export it from MetaMask.

Next, we import the private key that we've retrieved from MetaMask and store it in a `.json` file. This file should be created under the root directory, and named `private.json`. Because this key is highly sensitive information, it's very important that we are not revealing any information when deploying. To ensure this, we want to create a `.gitignore` file under our root directory. Then, you can ignore any files by using the format: `.filename` or any directories by using: `directory/`. In our case, we are trying to ignore our private key file so it should look like this:Add a caption

![](https://static.slab.com/prod/uploads/9yelyblh/posts/images/qYc7URDZvRQQOI3CbLlhSPNC.png)

The private.json file must contain a privateKey entry, for example:

{% tabs %}
{% tab title="private.json" %}
```typescript
{
  "privateKey": "YOUR-PRIVATE-KEY-HERE"
}
```
{% endtab %}
{% endtabs %}

Inside the `module.exports`, we need to provide the Solidity version (`0.8.1` according to our contract file), and the network details. Here, we are using test-net (Beresheet) network for the following example :

* Network name: Beresheet
* RPC URL: [https://beresheet2.edgewa.re/evm](https://beresheet2.edgewa.re/evm) (Alternatively, one can use [https://beresheetX.edgewa.re/evm](https://beresheetx.edgewa.re/evm) where X can be any number from 1 to 8.)
* Chain ID: 2022

If you want to deploy to a local Edgeware development node, you can use the following network details:

* Network name: dev
* RPC URL: [http://localhost:9933/](http://localhost:9933)
* Chain ID: 2021

If you want to deploy on the Edgeware mainnet, you can use the following network details:

* Network name: Edgeware
* RPC URL: [https://mainnet2.edgewa.re/evm](https://mainnet2.edgewa.re/evm) (Alternatively, one can use [https://mainnetX.edgewa.re/evm](https://mainnetx.edgewa.re/evm) where X can be any number from 1 to 20.)
* Chain ID: 2021

The Hardhat configuration file should look like this:

{% tabs %}
{% tab title="hardhat.config.js" %}
```typescript
// ethers plugin required to interact with the contract
require('@nomiclabs/hardhat-ethers');

// private key from the pre-funded Beresheet testing account
const { privateKey } = require('./private.json');

module.exports = {
  // latest Solidity version
  solidity: "0.8.1",

  networks: {
    // Beresheet network specification
    Beresheet: {
      url: `https://beresheet2.edgewa.re/evm`,
      chainId: 2022,
      accounts: [privateKey]
    }
  }
};
```
{% endtab %}
{% endtabs %}

Great! We are now ready for deployment.

Hardhat has some other cool features like helpful [stack trace](https://hardhat.org/hardhat-network/#solidity-stack-traces), support for [multiple Solidity compiler versions](https://hardhat.org/guides/compile-contracts.html#multiple-solidity-versions), robust [Mainnet forking](https://hardhat.org/hardhat-network/guides/mainnet-forking.html#mainnet-forking), great [TypeScript support](https://hardhat.org/guides/typescript.html#typescript-support), and contract verification in Ether scan.
