# Retrieve your ETH

{% tabs %}
{% tab title="Commonwealth Unlock Tool " %}
### Prerequisites

* The ETH address of the account you participated in the lockdrop with.
* A web3 Wallet with an account with enough ETH to cover the unlock transaction \(gas\) costs. 

### Steps

Visit the [Unlock tool at Commonwealth.im](https://commonwealth.im/edgeware/unlock)

Select the version of the Master Lockdrop Contract you used to participate in the Lockdrop event. 

* MLC v1 \(Old\) `0x1b75b90e60070d37cfa9d87affd124bb345bf70a`
* MLC v2 \(New\) `0xFEC6F679e32D45E22736aD09dFdF6E3368704e31`

If you are not sure which you used, examine the transactions at your participating ETH address using a block explorer for the locking transactions.

Enter your participating ETH address and hit "Get Locks" button.

View the LUC instances and select unlock to cue a Metamask or web3 wallet transaction. Send the transaction. 
{% endtab %}

{% tab title="Send a Transaction Manually" %}
### Prerequisites

* Access and control over the _original_ account you sent from when creating your LUC from the MLC - the ETH will be returned here.
* [Metamask](https://chrome.google.com/webstore/detail/metamask/nkbihfbeogaeaoehlefnkodbefgpgknn) or a wallet with transaction abilities with _any_ account connected, it _does not_ have to be the original, but it **does** need enough ETH to pay the 'gas' \(the transaction fee\) for the transaction - likely equal or less than 0.00042 ETH.
* The _contract_ address of your LUC. See link below if you need this.

{% page-ref page="finding-your-lockdrop-user-contract-luc.md" %}

### Steps

1. Open Metamask or wallet and select the account you want to pay the transaction fee from.
2. Hit the Send Button
3. Confirm that the account Selected at top has enough ETH to pay the transaction fee.
4. Carefully enter your LUC's Contract Address into the Recipient Address field.
5. Enter zero for the send amount.
6. Increase your gas limit on a transaction to 40k.
7. Confirm that your transaction speed \(and therefore transaction fee cost\) is satisfactory. \(More fee means quicker processing by the network.\)
8. Hit Next

Now watch for the transaction to be finalized, and confirm that your ETH arrived home safely.
{% endtab %}
{% endtabs %}





