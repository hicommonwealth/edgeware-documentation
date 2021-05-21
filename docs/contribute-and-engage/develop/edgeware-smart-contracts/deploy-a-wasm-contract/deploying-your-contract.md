# Deploying Your Contract

Now that we have generated the Wasm binary from our source code and started a Substrate node, we want to deploy this contract onto our Substrate blockchain.

Smart contract deployment on Substrate is a little different than on traditional smart contract blockchains.

Whereas a completely new blob of smart contract source code is deployed each time you push a contract on other platforms, Substrate opts to optimize this behavior. For example, the standard ERC20 token has been deployed to Ethereum thousands of times, sometimes only with changes to the initial configuration \(through the Solidity `constructor` function\). Each of these instances take up space on the blockchain equivalent to the contract source code size, even though no code was actually changed.

In Substrate, the contract deployment process is split into two halves:

1. Putting your code on the blockchain
2. Creating an instance of your contract  

With this pattern, contract code like the ERC20 standard can be put on the blockchain a single time, but instantiated any number of times. No need to continually upload the same source code over and waste space on the blockchain.

## Fast Track

If you skipped previous steps and just want to see interaction with ink! smart contract, download [flipper.wasm](https://contracts.edgewa.re/0/assets/flipper.wasm) and [metadata.json](https://contracts.edgewa.re/0/assets/flipper.json)

## Putting Your Code on the Blockchain

With your Substrate development node running, you can go back to the [Polkadot UI](https://polkadot.js.org/apps/) where you will be able to interact with your blockchain.

Under the **Developer** tab click on the specially designed [Contracts](https://polkadot.js.org/apps/?rpc=ws%3A%2F%2F127.0.0.1%3A9944#/contracts) section of the UI.

In the **Contracts** section, select **"Upload & deploy code"**.

![](https://user-images.githubusercontent.com/32852637/111106282-2ec9d800-852b-11eb-8e31-6a0af519f0fe.jpg)

In the popup, select a _**deployment account**_ with some account balance, like `Dave`. For the _**contract's metadata**_, select the JSON file. In _**compiled contract WASM**_, select the `flipper.wasm` file we generated. The code bundle name will be "flipper". Once all the parameters are filled, click **Next**. ![docsdeploy1](https://user-images.githubusercontent.com/32852637/111107417-2f636e00-852d-11eb-8fe4-2a665627685d.PNG)

## Creating an Instance of Your Contract

Smart contracts exist as an extension of the account system on the blockchain. Thus creating an instance of this contract will create a new `AccountId` which will store any balance managed by the smart contract and allow us to interact with the contract.

To instantiate our contract we just need to give this contract account an _**endowment**_ of `10 Units` in order to pay the storage rent and set the _**maximum gas allowed**_ to value\(`1,000,000`\):

![](https://user-images.githubusercontent.com/32852637/111108637-a69a0180-852f-11eb-8536-3172307771ed.PNG)

{% hint style="info" %}
**Note:** As mentioned earlier, contract creation involves creation of a new Account. As such, you must be sure to give the contract account at least the existential deposit defined by your blockchain. We also need to be able to pay the contract's rent \(**`endowment`**\). If we consume all of this deposit, the contract will become invalid. We can always refill the contract's balance and keep it on chain.
{% endhint %}

You will then **authorize** the contract, by **signing and submitting**. You can also choose to leave a tip for the block author if you'd like.

![](https://user-images.githubusercontent.com/32852637/111108711-ca5d4780-852f-11eb-8f27-b482aacabfeb.PNG)

When you press **Deploy**, you should see a flurry of events appear including the creation of a new account \(`system.NewAccount`\) and the instantiation of the contract \(`contracts.instantiate`\):

![](https://user-images.githubusercontent.com/32852637/111108864-0f817980-8530-11eb-9a43-da24dc192bfa.PNG)

