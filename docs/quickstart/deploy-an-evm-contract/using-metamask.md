# Using Metamask

<h2>Introduction</h2>

This guide will show you steps for using a self-contained Edgeware dev node to send tokens between EVM accounts with Metamask. To setup your own local node, learn more at this tutorial.

In this tutorial we will use the web3 rpc endpoints to interact with Edgeware.

<h2>Install the Metamask Extension</h2>

First, we start with a fresh and default [Metamask installation from the Chrome store](https://chrome.google.com/webstore/detail/metamask/nkbihfbeogaeaoehlefnkodbefgpgknn?hl=en). Follow the "Get Started" guide, where you need to create a wallet, set a password and store your secret backup phrase. (this gives direct access to your funds, so make sure to store these in a secure place).

<h2>Import Developer Account</h2>

Once completed, we will import our dev account. Click on upper right corner for accounts and hit `Import Account`:

<img width="900"  src="https://user-images.githubusercontent.com/32852637/111236536-743ce280-85c9-11eb-96a6-273cd4c4dc3c.png">

We have prefunded developer account for this purpose:

Private Key: `1111111111111111111111111111111111111111111111111111111111111111`

Address: `0x19e7e376e7c213b7e7e7e46cc70a5dd086daff2a`

On the import screen, select **"Private Key"** and paste there private key listed above and hit **Import:**

<img width="900"  src="https://user-images.githubusercontent.com/32852637/111236599-a2babd80-85c9-11eb-9499-093d763c3363.png">

You should see that account imported with wild balance (123456.123E) for our needs, in our case it's Account 4, it may differ in your enviroment.

<img width="900"  src="https://user-images.githubusercontent.com/32852637/111374108-1a90f280-8673-11eb-95ce-1d2ce679e676.png">

<h2>Connect to the Local Edgeware Developer Node</h2>

Now let's connect MetaMask to our locally running Edgeware EVM node. On upper right, hit Networks and click Custom RPC.

<img width="1121"  src="https://user-images.githubusercontent.com/32852637/111374246-4318ec80-8673-11eb-8061-e49c6dd762d0.png">

Put there credentials Network Name: `Edgeware EVM` New RPC URL: `http://127.0.0.1:9933` ChainID: `2021`

and hit **Save** button. Your can see it in figure below:

<img width="1121"  src="https://user-images.githubusercontent.com/32852637/111374364-6774c900-8673-11eb-8edf-b17ab413c160.png">

<h2>Make a Transfer</h2>

Now to verify your setup, you can try to make transfer between accounts. Don't worry, it's free! ;)

<img width="1121"  src="https://user-images.githubusercontent.com/32852637/111374451-81aea700-8673-11eb-8412-9dde10e408a9.png">

As new account, you should notice Nonce should be 0.

<img width="1121"  src="https://user-images.githubusercontent.com/32852637/111374503-92f7b380-8673-11eb-96f0-770efdc251e6.png">

Once is transaction in the block, you should see confirmed transaction like this:

<img width="1121"  src="https://user-images.githubusercontent.com/32852637/111374564-a571ed00-8673-11eb-88e1-8a4f185786e5.png">

<h2>Reach us for more engagement</h2>

Glad you've made it through! 🥰 We are eager to guide your more on your exploration through Edgeware Ethereum compability feature. We are **keen to hear your experience and suggestions you may have for us..** You can feel free to [chat with us in the Edgeware's channels like Discord, Element and Telegram](https://linktr.ee/edg_developers), we can help you out with issues you may have or project you may want to be funded through our [Treasury program](https://docs.edgewa.re/edgeware-runtime/treasury). Don't hesitate to share your feedback on our channels, there is always space to improve! 🙌





















