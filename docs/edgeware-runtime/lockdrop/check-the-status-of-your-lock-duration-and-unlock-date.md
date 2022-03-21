# Check the Status of Your Lock Duration and Unlock Date

There are two ways to check on your lock duration. The easiest way is through the Commonwealth Unlock or Lockdrop Stats tool, the other way requires that you look at the lock-initiating transaction on a block explorer.

{% tabs %}

Visit either

* [Commonwealth's Lockdrop Stats Tool](https://commonwealth.im/edgeware/stats)
* [Commonwealth's Unlock Tool](https://commonwealth.im/edgeware/unlock) \(Can also automate unlocking of ETH\)

Enter your participating ETH address to view all lockdrop user contracts associated with the address.

## Prerequisites

* The ETH address you locked from
* The transaction that you sent to trigger the lockdrop entry.

## Steps

Find the lock transaction in [a block explorer like Etherscan.io](http://etherscan.io), note the date of the send.

In the transaction details, find the Input Data \(see screenshot below,\) and find the segment that shows `[0]:0000000000 ...` and note the number at the end of the segment.

![](../../.gitbook/assets/screen-shot-2020-02-13-at-12.02.31-pm%20%281%29%20%281%29.png)

If that number is ..

`0` = A three month lock duration

`1` = A six month lock duration

`2` = A twelve month lock duration

Add the month value to the transaction date to find your unlock date and see if that date has passed yet. If so, your LUC is ready to release your ETH.

{% page-ref page="../../quickstart/retrieve-your-eth/" %}

### Example

For instance, in the screenshot above, the date is `June-15-2019`, and the lock duration is `2` , meaning 12 months. June 15, 2019 plus 12 months is a year later, or ~June 15, **2020.**

