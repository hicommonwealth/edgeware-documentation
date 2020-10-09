# Connect to a Wallet and Check Balance

## Connect Your Account

There are several ways to connect your existing account from the Lockdrop or other events to an account manager or wallet.

First, install the [Polkadot.js Browser Extension](https://github.com/polkadot-js/extension):

{% tabs %}
{% tab title="Polkadot.js Extension" %}
* On Chrome, install via [Chrome web store](https://chrome.google.com/webstore/detail/polkadot%7Bjs%7D-extension/mopnmbcafieddcagagdcbnhejhlodfdd)
* On Firefox, install via [Firefox add-ons](https://addons.mozilla.org/en-US/firefox/addon/polkadot-js-extension/) 
* You will need your seed phrase, a series of words.

Next, click the Orange P icon in your browser extension section.

Click the button stating "I have a pre-existing seed, import the account."

Enter your mnemonic phrase and hit the confirm button.

Next, visit [https://polkadot.js.org/apps/\#/explorer](https://polkadot.js.org/apps/#/explorer), ensure you are connected to t[he Edgeware network](https://github.com/hicommonwealth/edgeware-documentation/tree/17538a7582222618c79acf5151bd55ec9f372e91/docs/quickstart/networks.md) by clicking the top left network logo and selecting the network you want to connect to.

Once connected, the extension will prompt you to authorize connecting your local wallet to the service.Select your account, enter your wallet password and authorize the interaction.

You can now explore the chain and your account on Edgeware.

![](../.gitbook/assets/screen-shot-2020-02-10-at-3.03.43-am%20%281%29.png)
{% endtab %}

{% tab title="Commonwealth.im" %}
Finally, enter in a name and password twice for your newly connected account. Once connected, you can visit [https://polkadot.js.org/apps/\#/explorer](https://polkadot.js.org/apps/#/explorer), connect to the Edgeware testnet, and view your balance and interact with the chain.
{% endtab %}
{% endtabs %}

## Check your Balance via Block Explorer

At this time, the two main block explorers are

* [Polkascan](https://polkascan.io/pre/edgeware-berlin)
* [Subscan](https://edgeware.subscan.io/)

Both of these explorers will only work with Public Addresses \(SS58\) that have the Edgeware network ID encoded.

{% hint style="info" %}
If you have not re-encoded your public address from you Lockdrop-created keypair with the new Edgeware network ID, you **must do so** in order to use block explorers to find your account. Follow the instructions linked below.
{% endhint %}

Once you have your re-encoded Public Address, you can enter it into the search bar in a block explorer to pull up your account and view the balance.

