# Send EDG to another Account

{% tabs %}
{% tab title="Using Polkadot.js" %}
This method involves using the [Polkadot UI ](https://polkadot.js.org/apps/#/explorer)and the Polkadot.js browser extension.

You will need:

* ..to have [created an Edgeware account.]()
* ..to have installed [Polkadot.js to your browser and connected your wallet.](connect-an-account-to-a-wallet.md)
* Some [testnet ](https://github.com/hicommonwealth/edgeware-documentation/tree/17538a7582222618c79acf5151bd55ec9f372e91/docs/quickstart/ecosystem.md)or mainnet EDG to send. 

[Visit the Polkadot UI ](https://polkadot.js.org/apps/#/accounts)and ensure you are connected to the Edgeware network you want to participate in by clicking the network section in the top left. Once connected, click the Accounts tab in the left sidebar, or going directly to the Transfer tab.

In the Accounts tab, click the send button in the row of the account you want to send from.

![](../.gitbook/assets/screen-shot-2020-02-10-at-9.35.08-am%20%281%29.png)

Next, confirm the accounts you want to send from and send to, using the address fields. You can delete the information in the 'send to address' to enter in any recipient address, or utilize the dropdown to send between your own connected accounts in your Polkadot.js wallet.

Once the amount is entered and all the information is reviewed and confirmed \(treat cryptocurrency transactions as irreversible, so be careful,\) click "Make Transfer."

![](../.gitbook/assets/screen-shot-2020-02-10-at-9.39.14-am%20%281%29%20%281%29%20%281%29.png)

You will see a screen similar to this next, where you can see you transaction fees, can include a tip to the validator who authors the block for faster processing of the transaction \(uncommon,\) and otherwise confirm the send by signing the transaction.

Advanced: You can also pre-sign but _not_ submit this transaction to the network \(uncommon\) by using the bottom left 'Sign and Submit' toggle and entering a nonce and a duration for the validity of the signed transaction.

![](../.gitbook/assets/screen-shot-2020-02-10-at-9.43.14-am%20%281%29%20%281%29%20%281%29.png)

Once you hit sign and submit, your Polkadot.js browser extension will open a popup for your account password for the 'send from' account, and you will sign the transaction from your wallet.

![](../.gitbook/assets/screen-shot-2020-02-10-at-9.48.50-am%20%281%29.png)

Once you sign the transaction, the network receives it and you are done. You can explore the transaction details through a block explorer.
{% endtab %}

{% tab title="Using Commonwealth.im" %}
Coming soon.
{% endtab %}
{% endtabs %}

