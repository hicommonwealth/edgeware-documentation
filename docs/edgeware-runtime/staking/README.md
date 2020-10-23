# Staking

## Staking

Edgeware uses a version of proof-of-stake called Nominated Proof-of-Stake, and stakers are split into two types:

* **Validators:** Node operators who secure the network and are backed by nominators and their own stake.
* **Nominators:** EDG holders who delegate/nominate their EDG to a validator and share in the benefits.  

See more details about these roles below:

{% page-ref page="intro-to-roles-in-npos.md" %}

### Nominate

### Validate

Validation requires establishing a node, setting up your account and keys, and bonding EDG in order to verify blocks and secure the network. Follow these steps, in order, to get started.

## Staking and Consensus Parameters

**Reaping Threshold:** The amount that an account must maintain in order to avoid deletion.

#### **Consensus configuration**

* Aura 
* Runtime version: 28
* Blocktime: 6 seconds
* Session: 60 minutes \(600 blocks\)
* Era: 6 hours \(6 sessions per era\)

#### **Staking configuration**

* Validators at launch: 10
* Validator slots at launch: 60
* Bonding duration: [14 days](https://github.com/hicommonwealth/edgeware-node/blob/7405463cfecbe1aa2b185f365d7b0eec57f094f2/node/runtime/src/lib.rs#L420)
* Slashes deferred duration: 7 days
* Cancellation of slashes: 3/4 of council required - need to revisit this

