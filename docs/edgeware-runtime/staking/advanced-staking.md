# Advanced: Staking

## Staking

_This guide edited from the Polkadot Wiki with gratitude_

Edgeware uses NPoS \(Nominated Proof-of-Stake\) as its mechanism for selecting the validator set. It is designed with the roles of **validators** and **nominators**, to maximize chain security. Actors who are interested in maintaining the network can run a validator node. At genesis, Edgeware will have a limited amount of slots available for these validators, but this number will grow over time to over one thousand.

The system encourages EDG holders to participate as nominators. Nominators may back up to 16 validators as trusted validator candidates.

Validators assume the role of producing new blocks, validating blocks, and guaranteeing finality. Nominators can choose to back select validators with their stake.

The staking system pays out rewards equally to all validators. Distribution of the rewards are pro-rata to all stakers after the validator payment is deducted. In this way, the network incents the nomination of lower-staked validators to create an equally-staked validator set.

### How does staking work in Edgeware?

#### 1. Identifying which role you are

In staking, you can be either a [nominator or a validator](https://wiki.polkadot.network/docs/en/learn-staking#validators-and-nominators).

As a nominator, you can nominate one or more \(up to 16\) validator candidates that you trust to help you earn rewards in EDG. You can take a look at the [nominator guide](https://wiki.polkadot.network/docs/en/maintain-nominator) to understand what you are required to do when the mainnet launches.

A validator node is required to be responsive 24/7, perform its expected duties in a timely manner, and avoid any slashable behavior.

#### 2. Nomination period

Any potential validators can indicate their intention to be a validator candidate. Their candidacies are made public to all nominators, and a nominator in turn submits a list of any number of candidates that it supports. In the next epoch \(lasting several hours\), a certain number of validators having the most EDG backing get elected and become active. There are no particular requirements for a EDG holder to become a nominator, though we expect each nominator to carefully track the performance and reputation of validators.

Once the nomination period ends, the NPoS election mechanism takes the nominators and their associated votes as input, and outputs a set of validators of the required size, that maximizes the stake backing of any validator, and that makes the stakes backing validators as evenly distributed as possible. The objectives of this election mechanism are to maximize the security of the network, and achieve fair representation of the nominators. If you want to know more about how NPoS works \(e.g. election, running time complexity, etc.\), please read [here](http://research.web3.foundation/en/latest/polkadot/NPoS/).

#### 3. Staking Rewards Distribution

To explain how rewards are paid to validators and nominators, we need to consider **validator pools**, where a validator pool consists of an elected validator together with the nominators backing it. \(Note: if a nominator `n` with stake `s` backs several elected validators, say `k`, the NPoS election mechanism will split its stakes into pieces `s_1`, `s_2`, …, `s_k`, so that it backs validator `i` with stake `s_i`. In that case, nominator `n` will be rewarded the same as if there were `k` nominators in different pools, each backing a single validator `i` with stake `s_i`\). For each validator pool, we keep a list of nominators with the associated stakes.

The general rule for rewards across validator pools is that two validator pools get paid the **same amount of EDG** for equal work, i.e. they are NOT paid proportional to the stakes in each pool. Within a validator pool, a \(configurable\) part of the reward goes to pay the validator's commission fees and the remainder is paid **pro-rata** \(i.e. proportional to stake\) to the nominators and validator. Notice in particular that the validator is rewarded twice: once as commission fees for validating, and once for nominating itself with stake.

To estimate the inflation rate and how many EDG you can get each month as a nominator or validator, you can use this [Excel sheet](https://docs.google.com/spreadsheets/d/1-9Hc3kZ23EhZC3X6feRUKSTv6gj4xR7cvUbJD2zUEZk/edit?usp=sharing) as a reference and play around with it by changing some parameters \(e.g. validator pools, total supply, commission fees, etc.\) to have a better estimate. Even though it may not be entirely accurate since staking participation is changing dynamically, it works well as an indicator.

#### 4. Rewards Mechanism

We highlight two features of this payment scheme. The first is that since validator pools are paid the same, pools with less stake will pay more to nominators per-EDG than pools with more stake. We thus give nominators an economic incentive to gradually shift their preferences to lower staked validators that gain a sufficient amount of reputation. The reason for this is that we want the stake across validator pools to be as evenly distributed as possible, to avoid a concentration of power among a few validators. In the long term, we expect all validator pools to have similar levels of stake, with the stake being higher for higher reputation validators \(meaning that a nominator that is willing to risk more by backing a validator with a low reputation will get paid more\).

The following example should clarify the above. For simplicity, we have the following assumptions:

* These validators do not have a stake of their own.
* They do NOT charge any commission fees
* Reward amount is 100 EDG tokens
* The least amount of EDG to be a validator is 350

|  | **A - Validator Pool** |  |  |
| :--- | :--- | :--- | :--- |
| Nominator \(4\) | Stake \(600\) | Fraction of the Total Stake | Rewards |
| Jin | 100 | 0.167 | 16.7 |
| **Sam** | 50 | 0.083 | 8.3 |
| Anson | 250 | 0.417 | 41.7 |
| Bobby | 200 | 0.333 | 33.3 |

|  | **B - Validator Pool** |  |  |
| :--- | :--- | :--- | :--- |
| Nominator \(4\) | Stake \(400\) | Fraction of the Total Stake | Rewards |
| Alice | 100 | 0.25 | 25 |
| Peter | 100 | 0.25 | 25 |
| John | 150 | 0.375 | 37.5 |
| **Kitty** | 50 | 0.125 | 12.5 |

_Both validator pools A & B have 4 nominators with the total stake 600 and 400 respectively._

Based on the above rewards distribution, nominators in validator pool B get more rewards per EDG than those in pool A because pool A has more overall stake. Sam has staked 50 EDG in pool A, but he only gets 8.3 in return, whereas Kitty gets 12.5 with the same amount of stake.

We also remark that when the network slashes a validator slot for a misbehavior \(e.g. validator offline, equivocation, etc.\) the slashed amount is a fixed percentage \(and NOT a fixed amount of EDG\), which means that validator pools with more stake get slashed more EDG. Again, this is done to provide nominators with an economic incentive to shift their preferences and back less popular validators whom they consider to be trustworthy.

The second point to note is that each validator candidate is free to name their desired commission fee \(as a percentage of rewards\) to cover operational costs. Since validator pools are paid the same, pools with lower commission fees pay more to nominators than pools with higher fees. Thus, each validator can choose between increasing their fees to earn more EDG, or decreasing their fees to attract more nominators and increase their chances of being elected. We will let the market regulate itself in this regard. In the long term, we expect that all validators will need to be cost efficient to remain competitive, and that validators with higher reputation will be able to charge slightly higher commission fees \(which is fair\).

### Accounts

There are two different accounts for managing your funds: `Stash` and `Controller`.

![staking](https://wiki.polkadot.network/docs/assets/NPoS/staking-keys_stash_controller.png)

* **Stash:** This account holds funds bonded for staking, but delegates some functions to a Controller. As a result, you may actively participate with a Stash key kept in a cold wallet, meaning it stays offline all the time. You can also designate a Proxy account to vote in [governance](https://wiki.polkadot.network/docs/en/learn-governance) proposals.
* **Controller** This account acts on behalf of the Stash account, signalling decisions about nominating and validating. It set preferences like payout account and commission. If you are a validator, it also sets your [session keys](https://wiki.polkadot.network/docs/en/learn-keys#session-keys). It only needs enough funds to pay transaction fees.

We designed this hierarchy of separate key types so that validator operators and nominators can protect themselves much better than in systems with only one key. As a rule, you lose security anytime you use one key for multiple roles, or even if you use keys related by derivation. You should never use any account key for a "hot" session key in particular.

Controller and Stash account keys can be either sr25519 or ed25519.

### Validators and nominators

Since validator slots will be limited, most of those who wish to stake their DOTs and contribute economic security to the network will be nominators. Validators do most of the heavy lifting: they produce new block candidates, vote and come to consensus in GRANDPA, validate the STF of parachains, and possibly some other responsibilities regarding data availability and XCMP.

Nominators, on the other hand, do not need to do anything once they have bonded their EDG. The experience of the nominator is similar to "set it and forget it," while the validator will be doing active service for the network by performing the critical operations. For this reason, the validator has certain privileges regarding the payout of the staking mechanism and will be able to declare its own allocation before the share is divided to nominators.

![staking](https://wiki.polkadot.network/docs/assets/NPoS/article-2.png)

### Slashing

Slashing will happen if a validator misbehaves \(e.g. goes offline, attacks the network, or runs modified software\) in the network. They and their nominators will get slashed by losing a percentage of their bonded/staked EDG.

Validator pools with larger total stake backing them will get slashed more harshly than less popular ones, so we encourage nominators to shift their nominations to less popular validators to reduce the possible losses.

Based on Edgeware's latest codebase, the following slashing conditions have been implemented:

#### Unresponsiveness

For every session, validators will send an "I'm Online" message to indicate they are online. If a validator produces no blocks during an epoch and fails to send the heartbeat, it will be reported as unresponsive. Depending on the repeated offences and how many other validators were unresponsive or offline, slashing will occur.

Here is the formula for calculation:

```text
Let x = offenders, n = total no. validators

min((3 * (k - (n / 10 + 1))) / n, 1) * 0.07
```

Note that if less than 10% of all validators are offline, no penalty is enacted.

Validators should have a well-architected network infrastructure to ensure the node is running to reduce the risk of being slashed. A high availability setup is desirable, preferably with backup nodes that kick in **only once the original node is verifiably offline** \(to avoid double-signing and being slashed for equivocation - see below\), together with proxy nodes to avoid being DDoSed when your validator node's IP address is exposed. A comprehensive guide on secure validator setup is in progress with the draft available [here](https://wiki.polkadot.network/docs/en/maintain-guides-secure-validator).

**GRANDPA Equivocation:**  
A validator signs two or more votes in the same round on different chains.

GRANDPA equivocation slashing penalty is calculated as below:

```text
Let x = offenders, n = total no. validators

Min( (3 * x / n )^2, 1)
```

Validators may run their nodes on multiple machines to make sure they can still perform validation work in case one of their nodes goes down. It should be noted that if they do not have good coordination to manage signing machines, then equivocation is possible.

> Notice: If a validator is reported for any one of the offences they will be removed from the validator set and they will not be paid while they are kicked out.

If you want to know more details about slashing, please look at our [research page](https://research.web3.foundation/en/latest/polkadot/slashing/amounts.html).

### Reward Distribution

Rewards are recorded per session and paid per era.

#### Example

```text
    PER_ERA * BLOCK_TIME = **Reward Distribution Time**

    3600 * 6 seconds = 21,600 s = 6 hours

    ***These parameters can be changed by proposing a referendum***
```

Validators can create a cut of the reward that is not shared with the nominators. This cut is a percentage of the block reward, not an absolute value. After the value gets deducted, the remaining portion is based on their staked value and split between the validator and all of the nominators who have voted for this validator.

For example, assume the block reward for a validator is 10 EDG. A validator may specify `validator_payment = 50%`, in which case the validator would receive 5 EDG. The remaining 5 EDG would then be split between the validator and their nominators based on the proportion of stake each nominator had. Note that validators can put up their own stake, and for this calculation, their stake acts just as if they were another nominator.

Rewards can be directed to the same account \(controller\) or to the stash account \(and either increasing the staked value or not increasing the staked value\). It is also possible to top-up / withdraw some bonded EDG without having to un-stake everything.

## FAQs

### Why stake?

* 10% inflation/year when the network launches
* 50% targeted active staking
* ~20% annual return

### Why not stake?

* Tokens will be locked for 28 hours after unbonding. \(See Parameters page for most recent updated numbers\)
* Tokens can be slashed as punishment if the validator is not running properly.

### How many validators will Edgeware have?

The plan is to start with 60 open validator positions and open more gradually. The top bound on the number of validators has not been determined yet.

### Resources

* [How Nominated Proof of Stake will work in Polkadot](https://medium.com/web3foundation/how-nominated-proof-of-stake-will-work-in-polkadot-377d70c6bd43) - Blog post by Web3 Foundation researcher Alfonso Cevallos covering NPoS in Polkadot.
* [Secure validator setup](https://wiki.polkadot.network/docs/en/maintain-guides-secure-validator)

