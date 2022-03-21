---
description: Public Referenda Module
---

# Democracy

## `..From the Edgeware Whitepaper`

The democracy module creates and moves different binding referendum along the voting process.

Steps

* [Proposing Referenda](https://wiki.polkadot.network/docs/learn-governance#proposing-a-referendum) \(Involved info: [Referenda](https://wiki.polkadot.network/docs/learn-governance#referenda)\)
* [Voting on a Referendum](https://wiki.polkadot.network/docs/learn-governance#voting-on-a-referendum) \(Involved info: [Voluntary Locking](https://wiki.polkadot.network/docs/learn-governance#voluntary-locking)\)
* [Tallying](https://wiki.polkadot.network/docs/learn-governance#tallying) \(Involved info: [Adaptive Quorum Biasing](https://wiki.polkadot.network/docs/learn-governance#adaptive-quorum-biasing)\)

Referendums allows for the execution of an arbitrary extrinsic call on the chain as the root user.

This allows for execution of rather significant actions \(e.g. setting balance, modifying timestamps, etc\) without performing a runtime upgrade.

The module currently only supports binary supermajority-to-pass votes unless submitted by a council member \(which also supports supermajority-to-fail and simple majority\). Individuals vote on binary choice ballots that are tallied by coin-weight with lock-time adjustments. At the outset, all votes will be restricted to a two-week fixed period. In the future, the democracy module will be extended to many `VotingTypes.`

{% page-ref page="democracy-features.md" %}

