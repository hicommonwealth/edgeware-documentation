---
description: >-
  This guide will instruct token holders how to propose, delegate votes, and
  vote on public referenda using the Democracy module as it's implemented in
  Edgeware using the Polkadot UI.
---

# Guides to Referenda

The public referenda chamber is one of the two bodies of on-chain governance in Edgeware. The other body is the [council](https://wiki.polkadot.network/docs/en/maintain-guides-how-to-join-council).

1. Public referenda can be proposed and voted on by **any token holder in the system as long as they provide a bond**.
2. After a proposal is made, others can agree with it by _seconding_ it and putting up tokens equal to the original bond. 
3. Every launch period, the most seconded proposal will be moved to the public referenda table for active voting.

Voters who are willing to lock up their tokens for a greater duration of time can do so and get their vote amplified. For more details on the governance system please see [here](https://wiki.polkadot.network/docs/en/learn-governance).

{% hint style="info" %}
This guide will instruct token holders how to propose, delegate votes, and vote on public referenda using the Democracy module as it's implemented in Edgeware using [the Polkadot UI.](https://polkadot.js.org/apps/#/explorer)
{% endhint %}

## Important Parameters

The important parameters to be aware of when voting using the Democracry module are as follow:

{% hint style="info" %}
These parameters can change based on governance. Refer to [Network Parameters](https://docs.edgewa.re/understanding-edgeware/network-parameters#democracy-referenda) or the Node Runtime for the the most authoritative reference.
{% endhint %}

**Launch Period** - How often new public referenda are launched.

| Parameter | Value | Description |
| :--- | :--- | :--- |
| Launch Period | 7 days | How often new public referenda are selected by seconding actions and launched to the public for active vote. |
| Voting Period | 7 days | How often votes for referenda are tallied. |
| Emergency Voting Period | 3 days | The minimum voting period for a fast-tracked emergency referendum. \(aka Fast Track\) |
| Minimum Deposit | 100 EDG | The minimum amount to be used as a deposit for a public referendum proposal. |
| Enactment Period | 8 days | The minimum time period for locking funds _and_ the period between a proposal being approved and enacted |
| Cool off Period | 7 days | The time period where a proposal may not be re-submitted after being vetoed. |

\*\*\*\*

## Proposing an Action

Proposing an action to be taken requires you to bond some tokens. In order to ensure you have enough tokens to make the minimum deposit you can check the parameter in the chain state.

On Polkadot Apps you can use the "Democracy" tab to make a new proposal. In order to submit a proposal, you will need to submit what's called the preimage hash. The preimage hash is simply the hash of the proposal to be enacted. The easiest way to get the preimage hash is by clicking on the "Submit preimage" button and configuring the action that you are proposing.

For example, if you wanted to propose that the account "Dave" would have a balance of 10 tokens your proposal may look something like the below image. The preimage hash would be `0xa50af1fadfca818feea213762d14cd198404d5496bca691294ec724be9d2a4c0`. You can copy this preimage hash and save it for the next step. There is no need to click Submit Preimage at this point, though you could. We'll go over that in the next section.

![submit preimage](https://wiki.polkadot.network/docs/assets/democracy/submit_preimage.png)

Now you will click on the "Submit proposal" button and enter the preimage hash in the input titled "preimage hash" and _at least_ the minimum deposit into the "locked balance" field. Click on the blue "Submit proposal" button and confirm the transaction. You should now see your proposal appear in the "proposals" column on the page.

![submit proposal](https://wiki.polkadot.network/docs/assets/democracy/submit_proposal.png)

Now your proposal is visible by anyone who accesses the chain and others can second it or submit a preimage. However, it's hard to tell what exactly this proposal does since it shows the hash of the action. Other holders will not be able to make a judgement for whether they second it or not until someone submits the actual preimage for this proposal. In the next step you will submit the preimage.

![proposals](https://github.com/w3f/polkadot-wiki/blob/master/docs/assets/democracy/proposals.png)

## Submitting a Preimage

The act of making a proposal is split from submitting the preimage for the proposal since the storage cost of submitting a large preimage could be pretty expensive. Allowing for the preimage submission to come as a separate transaction means that another account could submit the preimage for you if you don't have the funds to do so. It also means that you don't have to pay so many funds right away as you can prove the preimage hash out-of-band.

However, at some point before the proposal passes you will need to submit the preimage or else the proposal cannot be enacted. The guide will now show you how to do this.

Click on the blue "Submit preimage" button and configure it to be the same as what you did before to acquire the preimage hash. This time, instead of copying the hash to another tab, you will follow through and click "Submit preimage" and confirm the transaction.

![submit preimage](https://wiki.polkadot.network/docs/assets/democracy/submit_preimage.png)

Once the transaction is included you should see the UI update with the information for your already submitted proposal.

![proposals updated](https://wiki.polkadot.network/docs/assets/democracy/proposals_updated.png)

## Seconding a Proposal

Seconding a proposal means that you are agreeing with the proposal and backing it with an equal amount of deposit as was originally locked. By seconding a proposal you will move it higher up the rank of proposals. The most seconded proposal - in value, not number of supporters - will be tabled as a referendum to be voted on every launch period.

To second a proposal, navigate to the proposal you want to second and click on the "Second" button.

![second button](https://wiki.polkadot.network/docs/assets/democracy/second_button.png)

You will be prompted with the full details of the proposal \(if the preimage has been submitted!\) and can then broadcast the transaction by clicking the blue "Second" button.

![second confirm](https://wiki.polkadot.network/docs/assets/democracy/second_confirm.png)

Once successful you will see your second appear in the dropdown in the proposal details.

![second result](https://wiki.polkadot.network/docs/assets/democracy/second_result.png)

## Voting on a Proposal

**Prerequisites to Vote:**

* Have an EDG Account
* Have EDG Tokens
* Be prepared to have **your EDG locked** during the duration of the referenda. \( Voting Period is 7 days\)
* Additionally, If you vote `aye` \('approve,' 'yes', 'in support'\) for a proposal and it passes, your tokens will be **locked** until the proposal has been enacted \(another 7 days.\)

{% hint style="info" %}
**Voting locks all of the tokens in the account you use to vote,** and weights your votes accordingly. In order to avoid having your entire EDG supply locked, create a separate voting account and transfer the amount you wish to vote with, over to that account first.
{% endhint %}

At the end of each launch period, the most seconded proposal will move to referendum. During this time you can cast a vote for or against the proposal. You may also lock up your tokens for a greater length of time to weigh your vote more strongly. During the time your tokens are locked, you are unable to transfer them, however they can still be used for further votes. Locks are layered on top of each other, so an eight week lock does not become a 15 week lock if you vote again a week later, rather another eight week lock is placed to extend the lock just one extra week.

To vote on a referendum, navigate to the ["Democracy" tab of Polkadot Apps](https://polkadot.js.org/apps/#/democracy/). Any active referendum will show in the "referenda" column. Click the blue button "Vote" to cast a vote for the referendum.

If you would like to cast your vote for the proposal select the "Aye, I approve" option. If you would like to cast your vote against the proposal in referendum you will select "Nay, I do not approve" option.

The second option is to select your conviction for this vote. The longer you are willing to lock your tokens, the stronger your vote will be weighted. Unwillingness to lock your tokens means that your vote only counts for 10% of the tokens that you hold, while the maximum lock up of 256 days means you can make your vote count for 600% of the tokens that you hold.

When you are comfortable with the decision you have made, click the blue "Vote" button to submit your transaction and wait for it to be included in a block.

![voting](https://wiki.polkadot.network/docs/assets/democracy/voting.png)

## Delegate a Vote

If you are too busy to keep up and vote on upcoming referenda, there is an option to delegate your vote to another account whose opinion you trust. When you delegate to another account, that account gets the added voting power of your tokens along with the conviction that you set. The conviction for delegation works just like the conviction for regular voting, except your tokens may be locked longer than they would normally since locking resets when you undelegate your vote.

The account that is being delegated to does not make any special action once the delegation is in place. They can continue to vote on referenda how they see fit. The difference is now when the Democracy system tallies votes, the delegated tokens now are added to whatever vote the delegatee has made.

You can delegate your vote to another account and even attach a "Conviction" to the delegation. Navigate to the "Extrinsics" tab on Polkadot Apps and select the options "democracy" and "delegate". This means you are accessing the democracy pallet and choosing the delegate transaction type to send. Your delegation will count toward whatever the account you delegated for votes on until you explicitly undelegate your vote.

In the first input select the account you want to delegate to and in the second input select the amount of your conviction. Remember, higher convictions means that your vote will be locked longer. So choose wisely!

![delegate](https://wiki.polkadot.network/docs/assets/democracy/delegate.png)

After you send the delegate transaction, you can verify it went through by navigating to the "Chain State" tab and selecting the "democracy" and "delegations" options. You will see an output similar to below, showing the addresses to which you have delegated your voting power.

![delegate state](https://wiki.polkadot.network/docs/assets/democracy/delegate_state.png)

## Undelegate a Vote

You may decide at some point in the future to remove your delegation to a target account. In this case, your tokens will be locked for the maximum amount of time in accordance with the conviction you set at the beginning of the delegation. For example, if you chose "2x" delegation for four weeks lock up time, your tokens will be locked for 4 weeks after sending the `undelegate` transaction. Once your vote has been undelegated, you are in control of making votes with it once again. You can start to vote directly, or chose a different account to act as your delegate.

The `undelegate` transaction must be sent from the account that you wish to clear of its delegation. For example, if Alice has delegated her tokens to Bob, Alice would need to be the one to call the `undelegate` transaction to clear her delegation.

The easiest way to do this is from the "Extrinsics" tab of Polkadot Apps. Select the "democracy" pallet and the "undelegate" transaction type. Ensure that you are sending the transaction from the account you want to clear of delegations. Click "Submit transaction" and confirm.

![undelegate](https://wiki.polkadot.network/docs/assets/democracy/undelegate.png)

## Proxies

Proxies can be used to vote on behalf of a stash account. Unlike delegation, the proxy is meant to act as a longer-term account that makes all the voting decisions for funds held in a different account. Delegation is a logical action, taken when you trust another account's judgement, while proxying is more of a recommended security practice for keeping your funds safe and using an active account with low funds instead.

### Setting a proxy

Setting a proxy involves submitting a single transaction, the transaction type "setProxy" from the "democracy" pallet.

You can make this transaction from Polkadot Apps by navigating to the "Extrinsics" tab and selecting the "democracy" pallet and the "setProxy" transaction type. Send the transaction from the "Stash" account which holds the funds that you want to vote with, and the target to the proxy account that will be responsible for casting the votes going forward. In the example below, "Alice Stash" is proxying to "Alice" so that Alice can vote on behalf of Alice Stash.

![set proxy](https://wiki.polkadot.network/docs/assets/democracy/set_proxy.png)

### Voting with a proxy

Making a vote on behalf of a stash requires a `proxyVote` transaction. When sending this transaction you will specify the index of the referendum that is being voted on as well as the judgement \(i.e. "Aye" for approval or "Nay" for rejection\).

![proxy vote](https://wiki.polkadot.network/docs/assets/democracy/proxy_vote.png)

### Removing a proxy

At some point you may want to remove a proxy from being able to vote on behalf of a stash account. This is possible to do by submitting a `removeProxy` transaction from the stash account, targetting the proxy account.

![remove proxy](https://wiki.polkadot.network/docs/assets/democracy/remove_proxy.png)

### Resigning a proxy

If a proxy account wants to resign their proxy status for a different stash account this is possible to do by sending the `resignProxy` transaction. Simply call this transaction from the proxy account and all of its proxy responsibilities will be removed.

![resign proxy](https://wiki.polkadot.network/docs/assets/democracy/resign_proxy.png)

