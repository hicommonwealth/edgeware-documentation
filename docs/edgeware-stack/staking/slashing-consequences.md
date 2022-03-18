# Slashing Consequences

[Learn more about Slashing](https://wiki.polkadot.network/docs/maintain-guides-validator-payout#slashing)

Slashing will happen if a validator misbehaves \(e.g. goes offline, attacks the network, or runs modified software\) in the network. They and their nominators will get slashed by losing a percentage of their bonded/staked EDG.

{% hint style="info" %}
Validator pools with larger total stake backing them will get slashed more harshly than less popular ones, so we encourage nominators to shift their nominations to less popular validators to reduce the possible losses.
{% endhint %}

Based on Substate's latest codebase, the following slashing conditions have been implemented:

### Unresponsiveness

For every session, validators will send an "I'm Online" message to indicate they are online. If a validator produces no blocks during an epoch and fails to send the heartbeat, it will be reported as unresponsive. Depending on the repeated offenses and how many other validators were unresponsive or offline, slashing will occur.

Here is the formula for calculation:

```text
Let x = offenders, n = total no. validators

min((3 * (k - (n / 10 + 1))) / n, 1) * 0.07
```

Note that if less than 10% of all validators are offline, no penalty is enacted.

Validators should have a well-architected network infrastructure to ensure the node is running to reduce the risk of being slashed. A high availability setup is desirable, preferably with backup nodes that kick in **only once the original node is verifiably offline** \(to avoid double-signing and being slashed for equivocation - see below\), together with proxy nodes to avoid being DDoSed when your validator node's IP address is exposed. A comprehensive guide on secure validator setup is in progress with the draft available [here](https://wiki.polkadot.network/docs/en/maintain-guides-secure-validator).

### GRANDPA Equivocation

A validator signs two or more votes in the same round on different chains.

### BABE Equivocation

A validator produces two or more blocks on the relay chain in the same time slot.

GRANDPA and BABE equivocation slashing penalty is calculated as below:

```text
Let x = offenders, n = total no. validators

Min( (3 * x / n )^2, 1)
```

Validators may run their nodes on multiple machines to make sure they can still perform validation work in case one of their nodes goes down. It should be noted that if they do not have good coordination to manage signing machines, then equivocation is possible.

> Notice: If a validator is reported for any one of the offences they will be removed from the validator set and they will not be paid while they are kicked out.

If you want to know more details about slashing, please look at our [research page](https://research.web3.foundation/en/latest/polkadot/slashing/amounts.html).

## Reward Distribution

Note that Kusama runs approximately 4x as fast as Polkadot, except for block production times. Polkadot will also produce blocks at approximately six second intervals.

Rewards are recorded per session --- approximately one hour on Kusama and four hours on Polkadot --- and paid per era. It takes approximately six hours to finish one era, twenty-four hours on Polkadot. Thus, rewards will be distributed to the validators and nominators four times per day on Kusama and once per day on Polkadot.

### Example

```text
    PER_ERA * BLOCK_TIME = **Reward Distribution Time**

    3600 * 6 seconds = 21,600 s = 6 hours

    ***These parameters can be changed by proposing a referendum***
```

Validators can create a cut of the reward that is not shared with the nominators. This cut is a percentage of the block reward, not an absolute value. After the value gets deducted, the remaining portion is based on their staked value and split between the validator and all of the nominators who have voted for this validator.

For example, assume the block reward for a validator is 10 DOTs. A validator may specify `validator_payment = 50%`, in which case the validator would receive 5 DOTs. The remaining 5 DOTs would then be split between the validator and their nominators based on the proportion of stake each nominator had. Note that validators can put up their own stake, and for this calculation, their stake acts just as if they were another nominator.

Rewards can be directed to the same account \(controller\) or to the stash account \(and either increasing the staked value or not increasing the staked value\). It is also possible to top-up / withdraw some bonded DOTs without having to un-stake everything.

## Inflation

