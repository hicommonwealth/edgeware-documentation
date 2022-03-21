---
description: >-
  This page is basically tips and tricks for councillors right now, so they
  understand to conduct.
---

# Council Operations and Resources

## Treasury

**When adopting a treasury proposal via Polkadot UI,** the 'Send to Council' Button may present the opportunity to set a 'threshold', or it may hardcode a threshold, currently believed to be 8.. This is a threshold of agreement, so if the threshold is 8, then 8 councilpeople must approve it, and then, only if that is fulfilled, the logic checks the on-chain parameters for other thresholds, supermajority, etc. If that also passes, then the treasury proposal now council motion is accepted and processed.

## Council Motions

* Motions to accept are separate from motions to reject, each is it's own standalone proposal.  
* Duplicate proposals are not accepted by the system while one is active.
* You can manipulate the threshold of Motions to reject to prevent easy rejections because a lower threshold version cannot be submitted, reason being that it is a duplicate.  This may be considered a bug, exploit, or other unintended use. 
* Threshold parameters can be set to force simple-majority or supermajority on motions that may normally need less consensus. 
* When submitting a motion, you must ensure that the threshold for that action according to the runtime parameters, &lt;= the threshold you submit. For example:
  * **Fail Case** Councilor Thom submits a Treasury.rejectProposal motion with a threshold of 1. Thom's vote is automatically counted as affirmative because he submitted the proposal. The threshold of 1 is met, and the motion attempts to execute.  However, the network runtime has a threshold of 2 for this action. The execution fails because the motion's job is done, but impermissible for the network, and nothing will go to the council. 

