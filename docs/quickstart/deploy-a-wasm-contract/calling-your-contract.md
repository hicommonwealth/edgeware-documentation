# Calling Your Contract

Now that your contract has been fully deployed, we can start to interact with it! Flipper only has two functions, so we will show you what it's like to play with both of them.

<h2>get()</h2>

If you take a look back at our contract's `on_deploy()` function, we set the initial value of the Flipper contract to `false`. Let's check that this is the case.

<img width="985"  src="https://user-images.githubusercontent.com/32852637/111218905-c243ed00-85ad-11eb-9641-60a0129c43cf.PNG">

<h2>flip()</h2>

So let's make the value `true` now!

The alternative **_message to send_** we can make with the UI is `flip()`. In this updated version, the contract will automatically estimate the neccesary **max gas allowed**. In this case, it's **674**. Leave estimated gas turned on, and **execute** the contract. In the following screen, authorize the transaction by clicking the `sign and submit` button.

<img width="983" src="https://user-images.githubusercontent.com/32852637/111219451-6af24c80-85ae-11eb-8785-1b9c649d22c1.PNG">

You will notice that this call actually sends a transaction. If the transaction was successful, we should then be able to go back to the `get()` function and see our updated storage:

<img width="1062" src="https://user-images.githubusercontent.com/32852637/111219508-83fafd80-85ae-11eb-961b-69bd7fc082bd.PNG">

Woohoo! You deployed your first smart contract!

<h2>Moving Forward</h2>

We will not go over these setup and deployment steps again, but we will use them throughout the tutorial. You can always come back to this chapter if you need to remember how to do a certain process.

The rest of the tutorial will have **template code** which you will use to walk through the different steps of contract development. Each template comes with a fully designed suite of tests that should pass if you programmed your contract correctly. Before you move on from a section, make sure that you run:

```
cargo +nightly test
```
and that the tests all execute successfully, without any warnings.

You need not deploy your contract between each section, but if we ask you to deploy your contract, you will need to follow the same steps you have done with the Flipper contract.



