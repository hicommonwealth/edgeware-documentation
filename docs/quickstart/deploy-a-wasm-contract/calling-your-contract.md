Calling Your Contract
===

Now that your contract has been fully deployed, we can start to interact with it! Flipper only has two functions, so we will show you what it's like to play with both of them.

## get()

If you take a look back at our contract's `on_deploy()` function, we set the initial value of the Flipper contract to `false`. Let's check that this is the case.

![An image of the Contracts call page](./assets/flipper-get.png)

## flip()

So let's make the value turn `true` now!

The alternative _message to send_ we can make with the UI is `flip()`. Again, set the _maximum gas allowed_ to `1,000,000`.

![An image of the Contracts extrinsic page](./assets/flipper-flip.png)

You will notice that this call actually sends a transaction. If the transaction was successful, we should then be able to go back to the `get()` function and see our updated storage:

![An image of Flipper RPC call with true](./assets/flipper-flip-true.png)

Woohoo! You deployed your first smart contract!

## Moving Forward

We will not go over these setup and deployment steps again, but we will use them throughout the tutorial. You can always come back to this chapter if you need to remember how to do a certain process.

The rest of the tutorial will have **template code** which you will use to walk through the different steps of contract development. Each template comes with a fully designed suite of tests that should pass if you programmed your contract correctly. Before you move on from a section, make sure that you run:

```bash
cargo +nightly test
```

and that the tests all execute successfully, without any warnings.

You need not deploy your contract between each section, but if we ask you to deploy your contract, you will need to follow the same steps you have done with the Flipper contract.
