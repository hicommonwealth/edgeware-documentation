# Using Web3

## Introduction <a id="introduction"></a>

This guide walks through the process of using Web3 to manually sign and send a transaction to a Edgeware EVM dev node. For this example, we will use Node.js and straightforward JavaScript code.

{% hint style="warning" %}
**Note** This tutorial was created using the release of Edgeware EVM. The Edgeware EVM platform, and the [Frontier](https://github.com/paritytech/frontier) components it relies on for Substrate-based Ethereum compatibility, are still under very active development. We have created this tutorial so you can test out Edgeware's Ethereum compatibility features. Even though we are still in development, we believe it’s important that interested community members and developers have the opportunity to start to try things with Edgeware and provide feedback.
{% endhint %}

### Checking Prerequisites <a id="checking-prerequisities"></a>

Installed [Nodejs](https://nodejs.org/en/) and particular package manager like [yarn](https://classic.yarnpkg.com/en/docs/install/#mac-stable) or [npm](https://www.npmjs.com/get-npm), rest we have batteries included in this tutorial. This guide assumes that you have a [running local Edgeware EVM node running in `--dev` mode.](https://docs.edgewa.re/contribute-and-engage/develop/edgeware-smart-contracts/deploy-an-evm-contract/setting-up-a-edgeware-evm-node).

```text
git clone https://github.com/edgeware-builders/tutorials tutorials;cd tutorials/web3;yarn
```

It will move to your cloned repository, install required packages and you are ready to go!

### Creating Transaction <a id="creating-transaction"></a>

For this example, we only need a single JavaScript file to create the transaction, which we will run using the `node` command in the terminal. The script will transfer 1337 ETH from the genesis account to another address. For simplicity, the file is divided into three sections: variable definition, create transactions and broadcast transaction.

We need to set a couple of values in the variables definitions:

* Create our Web3 constructor \(`web3`\)
* Define the `privKey` variable as the private key of our genesis account, which is where all the fund are stored when deploying your local Edgeware EVM node and what is used to sign the transactions
* Set the "from" and "to" address, making sure to set the value of `toAddress` to a different address, for example the one created by Metamask when setting up a local wallet

```javascript
const Web3 = require('web3');

// genesis private key
const privKey = '1111111111111111111111111111111111111111111111111111111111111111';
const addressFrom = '0x19e7e376e7c213b7e7e7e46cc70a5dd086daff2a';
const addressTo = '0x6bB5423f0Dd01B8C5028a1bc01e1f1bDe4523e72';
const web3 = new Web3('http://localhost:9933/');
```

Both the _create transaction_ and _deploy transaction_ sections are wrapped in an asynchronous function that handles the promises from our Web3 instance. To create the transaction, we use the `web3.eth.accounts.signTransaction(tx, privKey)` command, where we have to define the tx object with some parameters such as: `addressFrom`, `addressTo`, `number of tokens to send`, and the `gas limit`.

```javascript
const deploy = async () => {
  console.log(
    `Attempting to make transaction from ${addressFrom} to ${addressTo}`
  );

  const createTransaction = await web3.eth.accounts.signTransaction(
    {
      from: addressFrom,
      to: addressTo,
      value: web3.utils.toWei('1337', 'ether'),
      gas: 21000,
    },
    privKey
  );
```

Complete `createTransaction.js` should look like this!

```javascript
const Web3 = require('web3');

// genesis private key
const privKey = '1111111111111111111111111111111111111111111111111111111111111111';
const addressFrom = '0x19e7e376e7c213b7e7e7e46cc70a5dd086daff2a';
const addressTo = '0x6bB5423f0Dd01B8C5028a1bc01e1f1bDe4523e72';
const web3 = new Web3('http://localhost:9933/');

// Create transaction
const deploy = async () => {
  console.log(
    `Attempting to make transaction from ${addressFrom} to ${addressTo}`
  );

  const createTransaction = await web3.eth.accounts.signTransaction(
    {
      from: addressFrom,
      to: addressTo,
      value: web3.utils.toWei('1337', 'ether'),
      gas: 21000,
    },
    privKey
  );

  // Deploy transaction
  const createReceipt = await web3.eth.sendSignedTransaction(
    createTransaction.rawTransaction
  );
  console.log(
    `Transaction successful with hash: ${createReceipt.transactionHash}`
  );
  process.exit(0);
};

deploy();
```

### Check balance on accounts <a id="check-balance-on-accounts"></a>

Before running the script, we need another file to check the balances of both addresses before and after the transaction is executed. We can easily do this by leveraging the Ethereum compatibility features of Edgeware.

`balances.js` looks like this:

```javascript
const Web3 = require('web3');

// Variables definition
const addressFrom = '0x19e7e376e7c213b7e7e7e46cc70a5dd086daff2a';
const addressTo = '0x6bB5423f0Dd01B8C5028a1bc01e1f1bDe4523e72';
const web3 = new Web3('http://127.0.0.1:9933');

// Balance call
const balances = async () => {
  const balanceFrom = web3.utils.fromWei(
    await web3.eth.getBalance(addressFrom),
    'ether'
  );
  const balanceTo = await web3.utils.fromWei(
    await web3.eth.getBalance(addressTo),
    'ether'
  );

  console.log(`The balance of ${addressFrom} is: ${balanceFrom} ETH.`);
  console.log(`The balance of ${addressTo} is: ${balanceTo} ETH.`);
};

balances();Copy to clipboardErrorCopied
```

### Play time <a id="play-time"></a>

Run `node balance.js` to check initial balance on accounts

![](https://contracts.edgewa.re/4/assets/web3-init-balance.png) *web3-init-balance

Run `node createTransaction.js` to transfer some stuff around chain

![](https://contracts.edgewa.re/4/assets/web3-makeTransaction.png) *web3-make-transaction

Run `node balance.js` to check result balances

![](https://contracts.edgewa.re/4/assets/web3-result-balance.png) *web3-result-balance

### Reach us for more engagement <a id="reach-us-for-more-engagement"></a>

Glad you've made it through! 🥰 We are eager to guide your more on your exploration through Edgeware Ethereum combability feature. We are **keen to hear your experience and suggestions you may have for us.**. You can feel free to [chat with us in the Edgeware's channels like Discord, Element and Telegram](https://linktr.ee/edg_developers), we can help you out with issues you may have or project you may want to be funded through our [Treasury program](https://docs.edgewa.re/edgeware-runtime/treasury). Don't hesitate to share your feedback on our channels, there is always space to improve! 🙌

