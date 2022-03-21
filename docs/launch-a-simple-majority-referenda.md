---
description: A guide to executing a simple-majority public funding referenda
---

# Launch a Simple-Majority Referenda

_Credit:_ _Edited from_[\_ MrBulb's Commonwealth post.\_](https://commonwealth.im/edgeware/proposal/discussion/2423-how-to-execute-a-simplemajority-proposal)\_\_

Edgeware, through public discussion, has gained consensus to use '[SimpleMajority](https://commonwealth.im/edgeware/proposal/discussion/1563-simplemajority-a-proposed-edgeware-governance-standard)' for treasury funding as an Edgeware governance standard. A SimpleMajority proposal is one that only requires a majority - aka over 51% of votes to pass, instead of the default 'Supermajority' (2/3 of voters.) This ensures we have a bias for approval. Without this, the general will of many smaller holders can be easily overruled by a single party locking 6x against a proposal. In general, it is felt that this approach puts the power into the hands of the broader community, rather than individuals.

### **How to execute a SimpleMajority proposal**

The process is currently a little complicated, requiring a number of stages and council approval. Our aim is to automate this via adjustments to the existing treasury pallet.In the mean time, here's how you do it.

### Step 1 -Create a treasury proposal

Head to the [Polkadotjs app](https://polkadot.js.org/apps), switch to Edgeware and click into the [treasury tab ](https://polkadot.js.org/apps/#/treasury)which is located in the governance drop down menu. You will see the current treasury proposals:

![](https://commonwealth-uploads.s3.us-east-2.amazonaws.com/91d08008-ae62-4cb6-8cd6-60c47feecf1f.1635933888956)

Click the 'Submit Proposal' button on the right hand side of the interface and enter the details of the proposal. The 'submit with account' is required to bond 5% of the total requested EDG. You will have already setup a beneficiary account and added them to your [address book](https://polkadot.js.org/apps/#/addresses). In general with Edgeware we use a minimum of 2/3 multi-sig accounts for grants. You can find the multi-sig setup page on the [accounts](https://polkadot.js.org/apps/#/accounts) drop down menu.

![](https://commonwealth-uploads.s3.us-east-2.amazonaws.com/6427eb95-fdfe-4891-a691-b3c830b246b9.1635933721113)

On the next page there will be a "If submitted correctly, your treasury proposal will now enter the proposal queue. It will have a number assigned - in this case, the `proposalID` is **40**. This is important for the next stage

![](https://commonwealth-uploads.s3.us-east-2.amazonaws.com/7a9424d3-d9f2-46ff-aa55-93291f4145d8.1635934959775)

### Step 2 - Create a 'preimage' and accompanying 'hash'

Now we head to the Governance drop down menu and select [Democracy](https://polkadot.js.org/apps/#/democracy) and create a preimage of the proposal which is the formal key value description of the on-chain proposal.In the second box down select **treasury** from the list of options and this will give a few extra options. You want `approveProposal(proposalID)`Now enter the `proposalID` you received earlier - in this case\*\*,\*\* `40`**.**

Now copy the resulting **preimage hash**, and submit and sign this stage using your account.

**Step 3 - Council propose SimpleMajority as a motion**

The next stage involves a member of the council who will either be involved directly as they are the proposing party, or via a **network services agreement** such as Decent Partners, or indirectly as an intermediary to help a community member put forward a SimpleMajority proposal as a **Council motion**.

First we head to the **Developer** drop down menu and hit the [Extrinsics option](https://polkadot.js.org/apps/#/extrinsics).In this case I am proposing this SimpleMajority proposal therefore I need to switch to using my Council member account in the first box.

Then we select `Council` from the next drop down menu and `propose(threshold, proposal, lengthbound)`\*\* \*\*from the accompanying options.For threshold we select 8 - this means the SimpleMajority motion requires a minimum of 8 or the 13 Council members to pass and execute Treasury proposal 40 as a simple majority referendum.

In the next box down `proposal: Proposal`\*\* `` **select `democracy` and then next to that `externalProposeMajority (proposalHash)`**. \*\*

Into the box below `proposalHash: Hash` paste the **preimage hash** (the proposal hash) which you received in the previous part of the process.

For the final box, `lengthBound: Compact<u32>` enter **42**

Now hit **Submit Transaction**

![](https://commonwealth-uploads.s3.us-east-2.amazonaws.com/8ba414b8-eb6c-4a36-88d6-a3ec94a04085.1635939235332)

### Step 4 - Council approve SimpleMajority motion

Now 8/13 council members need to vote Aye to approve this motion and set the treasury proposal on the path to being a simplemajority referendum.

![](https://commonwealth-uploads.s3.us-east-2.amazonaws.com/c3f20370-5797-41eb-9ad3-555e056e156a.1635939332595)

When 8 have voted Aye, the motion can be closed, either by the original council member or any other council member including the last person to vote Aye. The motion will exist for 13 days, if we don't get enough votes Aye/Nay then it will not execute.If it does pass, then the proposal is on the road to becoming a simplemajority referendum where it will show up in the Governance drop down menu as an **external** proposal.

![](https://commonwealth-uploads.s3.us-east-2.amazonaws.com/f152dfd6-a18a-46a3-b06f-c1db8739962e.1635939756402)

![](https://commonwealth-uploads.s3.us-east-2.amazonaws.com/2edcae0d-4fde-4a13-9099-f9d66307fae1.1635937777381)
