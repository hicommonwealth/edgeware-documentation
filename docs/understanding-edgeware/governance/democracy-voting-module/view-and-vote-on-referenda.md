# View and Vote on Referenda

#### Where can I see current and past proposals?[¶](https://guide.kusama.network/en/latest/try/governance/#where-can-i-see-current-and-past-proposals) <a id="where-can-i-see-current-and-past-proposals"></a>

You can see active proposals you can vote on the [Polkadot UI](https://polkadot.js.org/apps/#/democracy) and [Commonwealth.im](https://commonwealth.im/edgeware). Viewing past proposals is not currently supported, but we will update this when we add that feature.

#### Viewing active referenda[¶](https://guide.kusama.network/en/latest/try/governance/#viewing-active-referenda) <a id="viewing-active-referenda"></a>

1. Using the [Polkadot UI](https://polkadot.js.org/apps/), make sure you have an account and **selected the Edgeware network** under the [settings tab](https://polkadot.js.org/apps/#/settings)
2. Navigate to the [Democracy tab](https://polkadot.js.org/apps/#/democracy) to see currently active proposals.



#### Voting on active referenda[¶](https://guide.kusama.network/en/latest/try/governance/#voting-on-active-referenda) <a id="voting-on-active-referenda"></a>

Voting on proposals in the Referendum chamber lasts 7 days and, if approved, then a further 7 days are waited before the change comes into force.

{% hint style="info" %}
**Parameter Note:** Voting Period, the length of time one may vote on a proposal, is 7 days. the Launch Period, or the delay until that vote's results become effective, is 7 days.
{% endhint %}

**Prerequisites to Vote:** 

* Have an EDG Account
* Have EDG Tokens
* Be prepared to have **your EDG locked** during the duration of the referenda. \( Voting Period is 7 days\)
* Additionally, If you vote `aye` \('approve,' 'yes', 'in support'\) for a proposal and it passes, your tokens will be **locked** until the proposal has been enacted \(another 7 days.\) 

{% hint style="info" %}
**Voting locks all of the tokens in the account you use to vote,** and weights your votes accordingly. In order not to have your entire EDG supply locked, create a separate voting account and transfer the amount you wish to vote with, over to that account first.
{% endhint %}

**Voting Using the Polkadot UI**

1. Using the [Polkadot UI](https://polkadot.js.org/apps/), make sure you have an account and selected the Edgeware network under the [settings tab](https://polkadot.js.org/apps/#/settings)
2. Navigate to the [Democracy tab](https://polkadot.js.org/apps/#/democracy) to see currently active proposals.
3. Note the proposal index number, and find out more details about the proposal at [Commonwealth.im/Edgeware](https://commonwealth.im/edgeware/)
4. Head over to the [Extrinsics tab](https://polkadot.js.org/apps/#/extrinsics), select the account you wish to vote with, and select `democracy` under "submit the following extrinsic." Choose `vote(ref_index,vote)` in the second column, enter the proposal index you noted down in step 3 and vote `aye` to support the proposal, and `nay` to vote against it.

**All the tokens in the account you selected will be locked until the referendum ends.** If you voted `aye` and the proposal has passed, your tokens will be locked until the proposal has been enacted in eight\* days. It is recommended that you do **not** vote with the entirety of your EDG, as your tokens will be locked up for some time, so **you should create a voting account** and transfer the amount of EDG you want to vote with before voting.

{% page-ref page="../../accounts/creating-an-account.md" %}



