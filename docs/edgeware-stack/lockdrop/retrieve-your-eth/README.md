---
description: A guide on retrieving ETH locked in the Edgeware lockdrop event.
---

# Retrieve your Locked ETH

There are two ways to retrieve your ETH from a lockdrop user contract:

* Using the Commonwealth unlock tool. (This tool is down occasionally.)
* Sending a manual transaction.

First, note the difference between a LUC and the MLC:

*   **Master Lockdrop Contract (MLC) (v1 and v2)**

    The coordinating contract that you sent your ETH to - it creates and sends this ETH on to your personal Lockdrop User Contract, which holds your ETH until unlock time. **Do not send the unlock transaction to an MLC - it will fail.**
* MLC v1 (Old) `0x1b75b90e60070d37cfa9d87affd124bb345bf70a`
* MLC v2 (New) `0xFEC6F679e32D45E22736aD09dFdF6E3368704e31`
* **Lockdrop User Contract (LUC)** Your individual lockdrop contract. This holds the ETH and is the contract you will use to unlock and retrieve your ETH. **This is where we will send an unlock transaction. See link below to find your LUC address.**

## Has your lock duration elapsed?

To retrieve your ETH, your lock duration must be complete or the transaction will fail. Before proceeding with this guide, check that your duration is over:

{% content-ref url="../check-the-status-of-your-lock-duration-and-unlock-date.md" %}
[check-the-status-of-your-lock-duration-and-unlock-date.md](../check-the-status-of-your-lock-duration-and-unlock-date.md)
{% endcontent-ref %}

{% tabs %}
{% tab title="Send a Transaction Manually" %}
### Prerequisites

* Access and control over the _original_ account you sent from when creating your LUC from the MLC - the ETH will be returned here.
* [Metamask](https://chrome.google.com/webstore/detail/metamask/nkbihfbeogaeaoehlefnkodbefgpgknn) or a wallet with transaction abilities with _any_ account connected, it _does not_ have to be the original, but it **does** need enough ETH to pay the 'gas' (the transaction fee) for the transaction - likely equal or less than 0.00042 ETH.
* The _contract_ address of your LUC. See above to learn how to find this.
* The unlock time must have passed for your LUC.

**Steps**

1. Open Metamask or wallet and select the account you want to pay the transaction fee from.
2. Hit the Send Button
3. Confirm that the account Selected at top has enough ETH to pay the transaction fee.
4. Carefully enter your LUC's Contract Address into the Recipient Address field.
5. Enter zero for the send amount.
6. Increase your gas limit on a transaction to 40k.
7. Confirm that your transaction speed (and therefore transaction fee cost) is satisfactory. (More fee means quicker processing by the network.)
8. Hit Next

{% hint style="info" %}
Unlock attempts fail due to three main reasons:

* The LUC is not yet past it's unlock date of 3, 6 or 12 months.
* The gas limit needs to be increased to 40k.
* You are attempting to send the transaction to an MLC and not your LUC.
{% endhint %}

Now watch for the transaction to be finalized, and confirm that your ETH arrived home safely.
{% endtab %}

{% tab title="Commonwealth Unlock Tool " %}
### Prerequisites

* The ETH address of the account you participated in the lockdrop with.
* Control over the account you originally participated in the lockdrop with - the ETH will return here.
* A web3 Wallet with an account with enough ETH to cover the unlock transaction (gas) costs.
* Your unlock time has elapsed.

{% hint style="info" %}
This tool may be offline or display errors due to Infura - if so, switch to the manual process in this guide.
{% endhint %}

### Steps

Visit the [Unlock tool at Commonwealth.im](https://commonwealth.im/edgeware/unlock)

Select the version of the Master Lockdrop Contract you used to participate in the Lockdrop event.

* MLC v1 (Old) `0x1b75b90e60070d37cfa9d87affd124bb345bf70a`
* MLC v2 (New) `0xFEC6F679e32D45E22736aD09dFdF6E3368704e31`

If you are not sure which you used, examine the transactions at your participating ETH address using a block explorer for the locking transactions.

Enter your participating ETH address and hit "Get Locks" button.

View the LUC instances and select unlock to cue a Metamask or web3 wallet transaction. Send the transaction.

{% hint style="info" %}
Unlock attempts fail due to two main reasons:

* The LUC is not yet past it's unlock date of 3, 6 or 12 months.
* The gas limit needs to be increased to 40k.
{% endhint %}
{% endtab %}
{% endtabs %}
