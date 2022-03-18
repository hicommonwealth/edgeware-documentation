# Using Metamask

## Introduction <a id="introduction"></a>

This guide will show you steps for using a self-contained Edgeware dev node to send tokens between EVM accounts with Metamask. To setup your own local node, learn more at this tutorial.

In this tutorial we will use the web3 rpc endpoints to interact with Edgeware

## Install the Metamask Extension <a id="install-the-metamask-extension"></a>

First, we start with a fresh and default [Metamask installation from the Chrome store](https://chrome.google.com/webstore/detail/metamask/nkbihfbeogaeaoehlefnkodbefgpgknn?hl=en). Follow the "Get Started" guide, where you need to create a wallet, set a password and store your secret backup phrase. \(this gives direct access to your funds, so make sure to store these in a secure place\).

## Import Developer Account <a id="import-developer-account"></a>

Once completed, we will import our dev account. Click on upper right corner for accounts and hit `Import Account`:

![](https://user-images.githubusercontent.com/32852637/121943618-c5bb5180-cd1f-11eb-9831-98412d203bdd.png)

We have prefunded developer account for this purpose:

Private Key: `1111111111111111111111111111111111111111111111111111111111111111`

Address: `0x19e7e376e7c213b7e7e7e46cc70a5dd086daff2a`

On the import screen, select **"Private Key"** and paste there private key listed above and hit **Import**:

![](https://user-images.githubusercontent.com/44712760/126711295-3cbfd0a9-c13b-43ee-9a69-a17ad106330e.png)

You should see that account imported with wild balance \(123456.123E\) for our needs, in our case it's **Edgeware Dev**, it may differ in your environment.

![Screen Shot 2021-07-20 at 6 53 51 AM](https://user-images.githubusercontent.com/44712760/126711489-424df67b-8dd8-4ea7-b4bb-4040e2bbcd0c.png)

## Connect to the Local Edgeware Developer Node <a id="connect-to-the-local-edgeware-developer-node"></a>

Now let's connect Metamask to our locally running Edgeware EVM node. The current network displayed is more than likely _'Ethereum mainnet'_. For our purposes, we'll want to change this: 1. Click the dropdown tab 2. Click `Custom RPC`.

![](https://user-images.githubusercontent.com/32852637/121945926-54c96900-cd22-11eb-92c3-48145a9c1352.png)

Put there credentials Network Name: `Edgeware EVM` New RPC URL: `http://127.0.0.1:9933` ChainID: `2021`

and hit **Save** button. Your can see it in figure below

![](https://user-images.githubusercontent.com/32852637/121949463-775d8100-cd26-11eb-84b3-133d225c23ea.PNG)

## Make a Transfer <a id="make-a-transfer"></a>

Now to verify your setup, you can try to make transfer between accounts. Don't worry, it's free! ;\)

As new account, you should notice Nonce should be 0

Once is transaction in the block, you should see confirmed transaction like this

![Screen Shot 2021-07-22 at 3 13 30 PM](https://user-images.githubusercontent.com/44712760/126711535-ae48be2c-9697-4fe7-89a4-1d6fddff2313.png)

## Reach us for more engagement <a id="reach-us-for-more-engagement"></a>

Glad you've made it through! 🥰 We are eager to guide your more on your exploration through Edgeware Ethereum compability feature. We are **keen to hear your experience and suggestions you may have for us.**. You can feel free to [chat with us in the Edgeware's channels like Discord, Element and Telegram](https://linktr.ee/edg_developers), we can help you out with issues you may have or project you may want to be funded through our <A HREF = "https://docs.edgeware.wiki/edgeware-stack/economics/treasury">Treasury program</A>. Don't hesitate to share your feedback on our channels, there is always space to improve! 🙌

