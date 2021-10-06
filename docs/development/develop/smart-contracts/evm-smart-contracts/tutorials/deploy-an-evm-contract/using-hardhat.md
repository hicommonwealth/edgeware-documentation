# Using Hardhat

{% hint style="danger" %}
**This page is still under development. Many functionalities of this page are still being worked on until further notice. To help our efforts, add a pull request with revised changes, thank you.**
{% endhint %}

![](https://user-images.githubusercontent.com/32852637/118346510-0437d380-b50a-11eb-9fc2-267d0b20777b.png)

## Interacting with Edgeware EVM using Hardhat

This guide walks through the process of deploying a **Solidity-based smart contract** to the Edgeware testnet Beresheet using Hardhat. [Hardhat](https://hardhat.org/) is a development environment to compile, deploy, test, and debug your Ethereum software. It helps developers manage and automate the recurring tasks that are inherent to the process of building smart contracts and dApps, as well as easily introducing more functionality around this workflow. This means compiling, running and testing smart contracts at the very core.

Hardhat comes built-in with **Hardhat Network**, a local Ethereum network designed for development. Its functionality focuses around Solidity debugging, featuring stack traces, console.log\(\) and explicit error messages when transactions fail.

**Hardhat Runner**, the CLI command to interact with Hardhat, is an extensible task runner. It's designed around the concepts of tasks and plugins. Every time you're running Hardhat from the CLI you're running a task. E.g. npx hardhat compile is running the built-in compile task. Tasks can call other tasks, allowing complex workflows to be defined. Users and plugins can override existing tasks, making those workflows customizable and extendable.

A lot of Hardhat's functionality comes from plugins, and, as a developer, you're free to choose which ones you want to use. Hardhat is unopinionated in terms of what tools you end up using, but it does come with some built-in defaults. All of which can be overridden.

To follow this tutorial you should be able to:

* [Write code in JavaScript](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/JavaScript_basics)
* [Operate a terminal](https://en.wikipedia.org/wiki/Terminal_emulator)
* [Use git](https://git-scm.com/doc)
* [Understand the basics of how smart contracts work](https://ethereum.org/learn/#smart-contracts)
* [Set up a Metamask wallet](https://metamask.io/)

## Installation

We need to install Node.js and npm package manager. You can download directly from Node.js or in your terminal.

{% tabs %}
{% tab title="Mac OS" %}
```text
# You can use homebrew (https://docs.brew.sh/Installation)
brew install node`

# Or you can use nvm (https://github.com/nvm-sh/nvm)
nvm install node
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Linux" %}
```text
curl -sL https://deb.nodesource.com/setup_15.x | sudo -E bash -

sudo apt install -y nodejs
```
{% endtab %}
{% endtabs %}

You can verify that everything is installed correctly by querying the version for each package:

`node -v`

`npm -v`

As of writing of this guide, the versions used were 15.7.0 and 7.4.3, respectively.

Also, you will need the following:

* Have MetaMask installed and connected to Beresheet
* Have an account with funds, which you can get from the automated bot on the Edgeware discord \(_in construction_\)

  To send funds to your meta mask you have to first convert your EVM address to a mainnet address. You can do so here at the bottom of the page [https://edgewa.re/keygen](https://edgewa.re/keygen) \(Convert Metamask/EVM address to mainnet address\)

Once all requirements have been met, you are ready to build with Hardhat.

## Starting a Hardhat Project

To start a new project, create a directory for it:

```text
mkdir EDGhat && cd EDGhat
```

Then, initialize the project by running:

```text
npm init -y
```

You will notice a newly created `package.json`, which will continue to grow as you install project dependencies.

To get started with Hardhat, we will install it in our newly created project directory:

```text
npm install hardhat
```

Once installed, run:

```text
npx hardhat
```

This will create a Hardhat config file \(hardhat.config.js\) in our project directory.

{% hint style="info" %}
`npx` is used to run executables installed locally in your project. Although Hardhat can be installed globally, we recommend installing locally in each project so that you can control the version on a project by project basis.
{% endhint %}

After running the command, choose `Create an empty hardhat.config.js` by using the arrow keys and enter:

![](https://user-images.githubusercontent.com/32852637/118343678-4bb56400-b4f8-11eb-9a04-8c70b28423a9.PNG)

## The contract file

We are going to store our contract in the `contracts` directory. Create it:

`mkdir contracts && cd contracts` or by creating a new directory under our root directory 'EDGHAT' in a text-editor such as [Visual Studio Code](https://code.visualstudio.com/)

{% hint style="info" %}
Editing directories in the terminal can be replicated in a text-editor at any point in this tutorial.
{% endhint %}

The smart contract that we'll deploy as an example will be called Box: it will let people store a value that can be later retrieved.

We will save this file as `contracts/Box.sol`:

```text
// contracts/Box.sol
pragma solidity ^0.8.1;

contract Box {
    uint256 private value;

    // Emitted when the stored value changes
    event ValueChanged(uint256 newValue);

    // Stores a new value in the contract
    function store(uint256 newValue) public {
        value = newValue;
        emit ValueChanged(newValue);
    }

    // Reads the last stored value
    function retrieve() public view returns (uint256) {
        return value;
    }
}
```

## Hardhat Configuration File

We need to modify our Hardhat configuration file so we can compile and deploy contracts into the Edgeware ecosystem. If you have not yet done so, connect your MetaMask Account to our ecosystem and fund it with the automated faucet bot on discord. We will use the private key of the account created to deploy the contract. If you don’t know the private key, you can export it from MetaMask.

We start by requiring the [ethers plugin](https://hardhat.org/plugins/nomiclabs-hardhat-ethers.html), which brings the \[ethers.js\]\[/integrations/ethers/\] library that allows you to interact with the blockchain in a simple way. We can install the ethers plugin by running:

```text
npm install @nomiclabs/hardhat-ethers ethers
```

Next, we import the private key that we've retrieved from MetaMask and store it in a `.json` file. This file should be created under the root directory, and named `private.json`. Because this key is highly sensitive information, it's very important that we are not revealing any information when deploying. To ensure this, we want to create a `.gitignore` file under our root directory. Then, you can ignore any files by using the format: `.filename` or any directories by using: `directory/`. In our case, we are trying to ignore our private key file so it should look like this:

![](https://user-images.githubusercontent.com/32852637/119069678-929dd080-b9b4-11eb-96d0-accb05d1666b.PNG)

The private.json file must contain a privateKey entry, for example:

```text
{
  "privateKey": "YOUR-PRIVATE-KEY-HERE"
}
```

Inside the `module.exports`, we need to provide the Solidity version \(`0.8.1` according to our contract file\), and the network details. Here, we are using testnet\(Beresheet\) network for the following example :

* Network name: Beresheet
* RPC URL: [https://beresheet2.edgewa.re/evm](https://beresheet2.edgewa.re/evm) \(Alternatively, one can use [https://beresheetX.edgewa.re/evm](https://beresheetX.edgewa.re/evm) where X can be any number from 1 to 8.\)
* Chain ID: 2022

If you want to deploy to a local Edgeware development node, you can use the following network details:

* Network name: dev
* RPC URL: [http://localhost:9933/](http://localhost:9933/)
* Chain ID: 2021

If you want to deploy on the Edgeware mainnet, you can use the following network details:

* Network name: Edgeware
* RPC URL: [https://mainnet2.edgewa.re/evm](https://mainnet2.edgewa.re/evm) \(Alternatively, one can use [https://mainnetX.edgewa.re/evm](https://mainnetX.edgewa.re/evm) where X can be any number from 1 to 20.\)
* Chain ID: 2021

The Hardhat configuration file should look like this:

```javascript
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

Great! We are now ready for deployment.

## Compiling Solidity

Our contract, `Box.sol`, uses Solidity 0.8.1. Make sure the Hardhat configuration file is correctly set up with this solidity version. If so, we can compile the contract by running:

```text
npx hardhat compile
```

![](https://user-images.githubusercontent.com/32852637/118344716-c92fa300-b4fd-11eb-86ff-c92ae08eb735.png)

After compilation, an `artifacts` directory is created: it holds the bytecode and metadata of the contract, which are `.json` files. It’s a good idea to add this directory to your `.gitignore`.

## Deploying the Contract

In order to deploy the Box smart contract, we will need to write a simple `deployment script`. First, let's create a new directory \(`scripts`\). Inside the newly created directory, add a new file `deploy.js`.

```text
mkdir scripts && cd scripts
touch deploy.js
```

Next, we need to write our deployment script using `ethers`. Because we'll be running it with Hardhat, we don't need to import any libraries.

We start by creating a local instance of the contract with the `getContractFactory()` method. Next, let's use the `deploy()` method that exists within this instance to initiate the smart contract. Lastly, we wait for its deployment by using `deployed()`. Once deployed, we can fetch the address of the contract inside the box instantiation.

```javascript
// scripts/deploy.js
async function main() {
   // We get the contract to deploy
   const Box = await ethers.getContractFactory('Box');
   console.log('Deploying Box...');

   // Instantiating a new Box smart contract
   const box = await Box.deploy();

   // Waiting for the deployment to resolve
   await box.deployed();
   console.log('Box deployed to:', box.address);
}

main()
   .then(() => process.exit(0))
   .catch((error) => {
      console.error(error);
      process.exit(1);
   });
```

Using the run command, we can now deploy the Box contract to Beresheet.

```text
npx hardhat run --network Beresheet scripts/deploy.js
```

{% hint style="info" %}
To deploy to an Edgeware development node, replace Beresheet for dev in the run command.
{% endhint %}

After a few seconds, the contract is deployed, and you should see the address in the terminal.

![](https://user-images.githubusercontent.com/32852637/119068621-8a449600-b9b2-11eb-8880-7cebaf9f41ee.PNG)

Congratulations, your contract is live! Save the address, as we will use it to interact with this contract instance in the next step.

## Interacting with the Contract

{% hint style="warning" %}
Limited functionality
{% endhint %}

Let's use Hardhat to interact with our newly deployed contract in Beresheet. To do so, launch hardhat console by running:

```text
npx hardhat console --network Beresheet
```

{% hint style="info" %}
To deploy to an Edgeware development node, replace Beresheet for dev in the run command.
{% endhint %}

Then, add the following lines of code one line at a time. First, we create a local instance of the `Box.sol` contract once again. Don't worry about the `undefined` output you will get after each line is executed:

```text
const Box = await ethers.getContractFactory('Box');
```

Next, let's connect this instance to an existing one by passing in the address we obtained when deploying the contract:

```text
const box = await Box.attach('ADDRESS-GOES-HERE');
```

After attaching it to the contract, we are ready to interact with it. While the console is still in session, let's call the store method and store a simple value:

```text
await box.store(5)
```

The transaction will be signed by your Beresheet account and broadcast to the network. The output should look similar to:

![](https://user-images.githubusercontent.com/32852637/118345245-2547f680-b501-11eb-9acf-189e876d7a69.png)

Notice your address labeled from, the address of the contract, and the data that is being passed. Now, let's retrieve the value by running:

```text
(await box.retrieve()).toNumber()
```

We should see `5` or the value you have stored initially.

Congratulations, you have completed the Hardhat tutorial!

For more information on Hardhat, hardhat plugins, and other exciting functionality, please visit [hardhat.org](https://hardhat.org).

