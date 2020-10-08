# Council

## Council

### Intro

Decentralized systems present a problematic scenario for online and active participation, often leading to low turnout. Therefore, council members can bias the quorum, the number of votes needed and the relative difference between affirmative and non-affirmative votes.

The Edgeware council module will eventually expand to allows 24 individual accounts to hold some exclusive rights over the network with council members having a fixed term of 12 months. At network launch, the number of council members will be thirteen. The council votes on a peer basis, that is, no coin-weighted votes.

Quorum biasing allows the council to change the effective supermajority required to make it easier or more difficult for a proposal to pass in the case that there is no clear majority of voting power backing it or against it. If all council members vote for a proposal, then the required amount of non-council member votes is lessened. The reverse also applies. When the council votes and more than one member dissents, then the quorum is negatively biased.

## Council Elections

#### How Council Members are Selected by the System

The Phragmen method is also used in the council election mechanism. When you vote for council members, you can select up to 16 different candidates, and then place a reserved bond which is the weight of your vote. Phragmen will run once on every election to determine the top candidates to assume council positions and then again amongst the top candidates to equalize the weight of the votes behind them as much as possible.

{% page-ref page="../../staking/the-sequential-phragmen-method.md" %}

### Council Operations and Resources

### Treasury

**When adopting a treasury proposal via Polkadot UI,** the 'Send to Council' Button may present the opportunity to set a 'threshold', or it may hardcode a threshold, currently believed to be 8.. This is a threshold of agreement, so if the threshold is 8, then 8 councilpeople must approve it, and then, only if that is fulfilled, the logic checks the on-chain parameters for other thresholds, supermajority, etc. If that also passes, then the treasury proposal now council motion is accepted and processed.

### Council Motions

* Motions to accept are separate from motions to reject, each is it's own standalone proposal.  
* Duplicate proposals are not accepted by the system while one is active.
* You can manipulate the threshold of Motions to reject to prevent easy rejections because a lower threshold version cannot be submitted, reason being that it is a duplicate.  This may be considered a bug, exploit, or other unintended use. 
* Threshold parameters can be set to force simple-majority or supermajority on motions that may normally need less consensus. 
* When submitting a motion, you must ensure that the threshold for that action according to the runtime parameters, &lt;= the threshold you submit. For example:
  * **Fail Case** Councilor Thom submits a Treasury.rejectProposal motion with a threshold of 1. Thom's vote is automatically counted as affirmative because he submitted the proposal. The threshold of 1 is met, and the motion attempts to execute.  However, the network runtime has a threshold of 2 for this action. The execution fails because the motion's job is done, but impermissible for the network, and nothing will go to the council. 

