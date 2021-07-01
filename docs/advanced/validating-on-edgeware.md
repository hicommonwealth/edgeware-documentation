# Validating on Edgeware

Welcome to the official, in-depth Edgeware guide to validating. We're happy that you're interested in validating on Edgeware and we'll do our best to provide in-depth documentation on the process below. As always, reach out on [Discord](https://discord.gg/CJRfb3) or [Telegram](https://t.me/heyedgeware) if you have questions about the project.

This document contains all the information one should need to start validating on Edgeware using the [**polkadot-js/apps user interface**](https://polkadot.js.org/apps/#/). We will start with how to setup one's node and proceed to how to key management and monitoring. To start, we will use the following terminology of keys for the guide:

* _**stash**_ - the stash keypair is where most of your funds should be located. It can be kept in cold storage if necessary.
* _**controller**_ - the controller is the keypair that will control your validator settings. It should have a smaller balance, e.g. 10-100 EDG
* _**session**_ - the 3 session keypairs are hot keys that are stored on your validator node. They do not need to have balances.

## Requirements

1. You should have balances in your `stash` \(ed25519 or sr25519\) and `controller` \(ed25519 or sr25519\) accounts.
2. Instructions for setting up a node are [here](https://github.com/hicommonwealth/edgeware-node/wiki/Setting-up-a-Node). You will need to additionally add the `--validator` flag to run a validator node.
3. You should have a wallet, such as the `polkadot-js` extension, installed in your browser with the stash and controller keypairs. If you don't have it, get it [here](https://github.com/polkadot-js/extension).

If you need to request a testnet EDG balance, just ask on [Discord](https://github.com/Edgeware-Network/edgeware-documentation/tree/815a72388a9df65c3db9f048eaed42ea8f645780/docs/advanced-topics/1/README.md).

### 1. Install the Edgeware node

If you are starting a validator node that needs to stay up, we recommend [following the default instructions](https://github.com/hicommonwealth/edgeware-node/wiki/Setting-up-a-Node) and [setting up monitoring](https://github.com/hicommonwealth/edgeware-node/wiki/Setting-up-monitoring).

Then, you should go to the line where `target/release/edgeware` is called in `/etc/systemd/system/edgeware.service`, and add the `--validator` flag. Reload the service configuration and check to see the node has started properly:

```text
systemctl daemon-reload
systemctl restart edgeware
systemctl status edgeware
```

You should see this output:

```text
2019-10-03 10:28:59 Edgeware
2019-10-03 10:28:59   version 1.0.0-3f34fba-x86_64-macos
2019-10-03 10:28:59   by Commonwealth Labs, 2018-2019
2019-10-03 10:28:59 Chain specification: Edgeware
2019-10-03 10:28:59 Node name: naughty-light-7646
2019-10-03 10:28:59 Roles: AUTHORITY
```

**Make sure the Chain specification is correct, and the node is running with `Roles: AUTHORITY.`** If you don't see the correct Chain, you should provide the correct `--chain` parameter, and if you don't see the Authority role, you should make sure you're actually running Edgeware with the `--validator` flag.

**Make sure you can access the node through the command line.** If you enter the `curl` command below, you should see this output:

```text
curl --include --no-buffer --header "Connection: Upgrade" --header "Upgrade: websocket" --header "Sec-WebSocket-Key: SGVsbG8sIHdvcmxkIQ==" --header "Sec-WebSocket-Version: 13" localhost:9944

HTTP/1.1 101 Switching Protocols
Connection: Upgrade
Sec-WebSocket-Accept: qGEgH3En71di5rrssAZTmtRTyFk=
Upgrade: websocket
```

**Check the** [**telemetry dashboard**](https://github.com/hicommonwealth/edgeware-node/wiki)**, and make sure your node is syncing up to the latest block.** If any of these steps do not check out, stop now; you will not be able to validate until they are corrected.

### 2. Connect via the interface

Go to the [polkadot-js web interface](https://polkadot.js.org/apps/#/settings) and connect to a custom node, e.g. testnet1.edgewa.re, testnet2.edgewa.re, or testnet3.edgewa.re.

The interface should show the correct latest block.

### 3. Create a stake

Go to the **Staking** tab, and select **Account actions** at the top. Click on **New stake**.

Select your controller and stash accounts. Enter how much of your stash balance you would like to stake. Leave a few EDG free, or you will be unable to send transactions from the account.

You can also choose where your validator rewards are deposited \(to the stash or the controller\) and whether rewarded EDG should be automatically re-staked.

![Enter stake amount](https://user-images.githubusercontent.com/1273926/66247046-d5227480-e6cd-11e9-9ddf-45af83a102d4.png)

Sign and send the transaction.

### 4. Set your session keys, using `rotateKeys`

Click on **Set Session Keys** on the stake you just created above.

Go to the command line where your validator is running \(e.g. SSH into the server, etc.\) and enter this command. It will tell your validator to generate a new set of session keys:

```text
curl -H 'Content-Type: application/json' --data '{ "jsonrpc":"2.0", "method":"author_rotateKeys", "id":1 }' localhost:9933
```

The output should look like this:

```text
{"jsonrpc":"2.0","result":"0x0ca0fbf245e4abca3328f8bba4a286d6cb1796516fcc68864cab580f175e6abd2b9107003014fc6baab7fd8caf4607b34222df62f606248a8a592bcba86ff9eec6e838ae8eb757eb77dffc748f1443e60c4f7617c9ea7905f0dd09ab758a8063","id":1}
```

Copy the hexadecimal key from inside the JSON object, and paste it into the web interface.

![rotateKeys input](https://user-images.githubusercontent.com/1273926/66247154-ca1c1400-e6ce-11e9-9a50-11b9a6734867.png)

Sign and send the transaction.

### 5. Start validating

![Validate or nominate](https://user-images.githubusercontent.com/1273926/66247159-cf795e80-e6ce-11e9-888b-63f870c301e9.png)

You should now see a **Validate** button on the stake. Click on it, and enter the commission you would like to charge as a validator. Sign and send the transaction.

You should now be able to see your validator in the **Next up** section of the staking tab.

At the beginning of the next **era**, if there are open slots and your validator has adequate stake supporting it, your validator will join the set of active validators and automatically start producing blocks. \(On the testnet, sessions are 100 blocks or 10 minutes long, and eras are 300 blocks or 30 minutes long.\)

Active validators receive rewards at the end of each era. Slashing also happens at the end of each era.:

![Reward](https://user-images.githubusercontent.com/1273926/66247183-e455f200-e6ce-11e9-93ba-5eee38b7c606.png)

Is your validator not producing blocks?

* Check that it is part of the active validator set. You will need to wait until your validator rotates in; this may take longer depending on whether there are free slots.
* Check that it is running with the `--validator` flag.
* Ensure your session keys are set correctly. Use `curl` to rotate your session keys again, and then send another transaction to the network to set the new keys.

### 6. Stop validating

If you would like to stop validating, you should use the **Stop Validating** button on your stake, to send a `chill` transaction. It will take effect when the next validator rotation happens, at which point you can shut down your validator.

Once you have stopped validating, you can send a transaction to unbond your funds. You can then **redeem** your unbonded funds after the unbonding period has passed.

![Unbond](https://user-images.githubusercontent.com/1273926/66247294-ee2c2500-e6cf-11e9-93a1-89e9fa532367.png)

![Redeem unbonded funds](https://user-images.githubusercontent.com/1273926/66247295-eec4bb80-e6cf-11e9-96a8-92ecbdc932d1.png)

