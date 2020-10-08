---
description: 'https://wiki.polkadot.network/docs/en/maintain-guides-how-to-vote-councillor'
---

# Voting for Council

## Intro <a id="__docusaurus"></a>

The council is an elected body of on-chain accounts that are intended to represent the passive stakeholders of Edgeware. The council has two major tasks in governance: proposing referenda and vetoing dangerous or malicious referenda. This guide will walk you through voting for councillors in the elections.

### Voting for Councillors

Voting for councillors requires you to lock your EDG for the duration of your vote. Like the validator elections, you can approve up to 16 different councillors and your vote will be equalized among the chosen group. Unlike validator elections, there is no unbonding period for your reserved tokens. Once you remove your vote, your tokens will be liquid again.

> Warning: It is your responsibility not to put your entire balance into the reserved value when you make a vote for councillors. It's best to keep _at least_ a few KSM to pay for transaction fees.

Go to the [Polkadot Apps Dashboard](https://polkadot.js.org/apps), **connect to the Edgeware endpoint**, and click on the "Council" tab. On the right side of the window there are two blue buttons, click on the one that says "Vote."

![](https://wiki.polkadot.network/docs/assets/council/vote.png)

Since the council uses approval voting, when you vote you signal which of the validators you approve of and your voted tokens will be equalized among the selected candidates. Select up to 16 council candidates by moving the slider to "Aye" for each one that you want to be elected. When you've made the proper configuration submit your transaction.

#### Voting for council members[¶](https://guide.kusama.network/en/latest/try/governance/#voting-for-council-members) <a id="voting-for-council-members"></a>

1. Using the [Polkadot UI](https://polkadot.js.org/apps/), make sure you have an account and selected the Kusama network under the [settings tab](https://polkadot.js.org/apps/#/settings).
2. Navigate to the [Council tab](https://polkadot.js.org/apps/#/council) to see current council candidates.
3. In the [Kusama forum](https://forum.kusama.network/), you will find a thread dedicated to council members proposing their candidacy and find out more information.
4. Head over to the [Extrinsics tab](https://polkadot.js.org/apps/#/extrinsics), select the account you wish to vote with, and select `council` under "submit the following extrinsic." Choose `setApprovals(votes, index)` in the second column, enter the council index of the candidate you wish to vote for, and select `yes` to support the candidate, and `nay` to vote against it.
5. Click `Submit transaction` and sign the transaction.

![](https://wiki.polkadot.network/docs/assets/council/vote_for_yourself.png)

You should see your vote appear in the interface immediately after your transaction is included.

### Removing your Vote

In order to get your reserved tokens back, you will need to remove your vote. Only remove your vote when you're done participating in elections and you no longer want your reserved tokens to count for the councillors that you approve.

Go to the "Extrinsics" tab on [Substrate Apps Dashboard](https://polkadot.js.org/apps).

Choose the account you want to remove the vote of and select the "electionsPhragmen -&gt; removeVoter\(\)" options and submit the transaction.

![](https://wiki.polkadot.network/docs/assets/council/remove_vote.png)

When the transaction is included in a block you should have your reserved tokens made liquid again and your vote will no longer be counting for any councillors in the elections starting in the next term.

