# Run For Council

## Intro

The council is an elected body of on-chain accounts that are intended to represent the passive stakeholders of the Edgeware network. The council has two major tasks in governance: proposing referenda and vetoing dangerous or malicious referenda. This guide will walk you through entering your candidacy to the council.

## Submit Candidacy

Submitting your candidacy for the council requires a bond of 1000 EDG.

{% hint style="info" %}
**Parameter Note:** The Candidacy Bond, or the current minimum bond to submit candidacy is 1000 EDG.
{% endhint %}

The bond will be forfeited if your candidacy does not win or become a runner-up, but if you become a member of the council you will eventually get your bond back. Runner-ups are selected after every round and are reserved members in case one of the winners gets forcefully removed.

It is a good idea to announce your council intention before submitting your candidacy so that your supporters will know when they can start to vote for you. You can also vote for yourself in case no one else does.

Go to [Polkadot Apps Dashboard](https://polkadot.js.org/apps), **connect to the Edgeware endpoint**, and navigate to the "Council" tab. Click the button on the right that says "Submit Candidacy."

### Steps to run for Council[¶](https://guide.kusama.network/en/latest/try/governance/#submit-oneself-as-a-council-candidate)

1. Using the [Polkadot UI](https://polkadot.js.org/apps/), make sure you have an account and selected the Kusama network under the [settings tab](https://polkadot.js.org/apps/#/settings).
2. Navigate to the [Council tab](https://polkadot.js.org/apps/#/council) to see current council candidates.
3. In the [Kusama forum](https://forum.kusama.network/), you will find a thread dedicated to council members proposing their candidacy and find out more information. Add your account number, reasons for being a suitable council member and any further information you want to share.
4. Head over to the [Extrinsics tab](https://polkadot.js.org/apps/#/extrinsics), select the account you wish to vote with, and select `council` under "submit the following extrinsic." Choose `submitCandidacy(slot)` in the second column and select the slot you prefer to be in.
5. Click `Submit transaction` and sign the transaction.

![a](https://wiki.polkadot.network/docs/assets/council/submit_candidacy.png)

After making the transaction, you will see your account appear on the right column under "Candidates."

![b](https://wiki.polkadot.network/docs/assets/council/candidate.png)

It is a good idea now to lead by example and give yourself a vote.

### Voting on Candidates

Next to the button to submit candidacy is another button titled "Vote." You will click this button to make a vote for yourself \(optional\).

![c](https://wiki.polkadot.network/docs/assets/council/vote.png)

The council uses the [Phragmen](https://wiki.polkadot.network/docs/en/learn-phragmen) approval voting which is also used in the validator elections. This means that you can choose up to 16 distinct candidates to vote for and your stake will equalize between them. For this guide, choose to approve your own candidacy by clicking on the switch next to your account and changing it to say "Aye."

![d](https://wiki.polkadot.network/docs/assets/council/vote_for_yourself.png)

### Winning an Election

If you are one of the lucky ones to win a council election you will see your account move to the left column under the heading "Members."

![e](https://wiki.polkadot.network/docs/assets/council/member.png)

Congratulations! Now you are able to participate on the council by making motions or vetoing proposals. It's a good idea to now add an Identity so that others know who the account belongs to and[ join the Commonwealth Edgeware forum.](https://commonwealth.im/edgeware/discussions)

