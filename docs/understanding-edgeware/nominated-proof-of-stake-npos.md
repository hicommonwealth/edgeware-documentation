---
description: >-
  The following resources on nPoS are gratefully utilized and edited from
  Research at W3F -
  https://research.web3.foundation/en/latest/polkadot/NPoS/index.html
---

# Nominated Proof-of-Stake  \(nPoS\)

Edgeware uses nominated proof-of-stake \(NPoS\), a relatively new type of scheme used to select the validators who are allowed to participate in the consensus protocol. We also explain the peculiar way in which validators get elected. 

## Validators and nominators <a id="validators-and-nominators"></a>



### Validators

A couple of times per day, the system elects a group of entities called **validators**, who in the next few hours will play a key role in highly sensitive protocols such as block production block finality. Their job is demanding as they need to run costly operations, ensure high communication responsiveness, and build a long-term reputation of reliability. They also must stake their EDG, Edgeware’s native token, as a guarantee of good behavior, and this stake gets slashed whenever they deviate from their protocol. In contrast, they get paid well when they play by the rules. Any node that is up to the task can publicly offer itself as a validator candidate. However, for operational reasons only a limited number of validators can be elected, expected to be hundreds or thousands.

{% hint style="info" %}
Validators are rewarded for running complex technical operations, and lose their staked EDG for misbehaving. Edgeware initially allows 60 Validator slots, but this number can change through governance actions.
{% endhint %}

### Nominators

The system also encourages **any** EDG holder to participate as a **nominator**. A nominator publishes a list of validator candidates that they trust, and puts down an amount of EDG at stake to support them with. If some of these candidates are elected as validators, she shares with them the payments, or the sanctions, on a per-staked-EDG basis. Unlike validators, an _unlimited_ number of parties can participate as nominators. As long as a nominator is diligent in their choice and only supports validator candidates with good security practices, the role carries low risk and provides a continuous source of revenue. 

## The NPoS scheme[¶]() <a id="the-npos-scheme"></a>

This nominator-validator arrangement gives strong security guarantees. It allows for the system to select validators with massive amounts of aggregate stake — much higher than any single party’s EDG holdings — and eliminate candidates with low stake. In fact, at any given moment we expect there to be a considerable fraction of all the EDG supply be staked in NPoS. This makes it very difficult for an adversarial entity to get validators elected \(as they need to build a fair amount of **reputation** to get the required backing from nominators\) and also very costly to attack the system if they do get elected \(because any attack will result in large amounts of EDG being slashed.

{% hint style="info" %}
"Slashing" is the loss or taking of some staked EDG and transferring it to the Edgeware Treasury. 
{% endhint %}

Our NPoS scheme is much more efficient than proof-of-work \(PoW\) and faster than standard proof-of-stake \(PoS\). Networks with deterministic finality must have a limited validator set \(the size can be changed with governance\). NPoS allows for virtually all EDG holders to continuously participate, thus maintaining high levels of security by putting more value at stake and allowing more people to earn a yield based on their holdings.

{% hint style="info" %}
Through nomination, all EDG holders, not merely technically-capable validators, can participate in securing the network and benefitting from rewards. 
{% endhint %}

## The Validator Election process[¶]() <a id="the-election-process"></a>

How to elect the validators, given the nominators’ votes? Unlike other PoS-based projects where validators are weighted by stake, NPoS gives elected validators equal voting power in the consensus protocol. 

To achieve proportional representation regardless of that fact, the total pool of their nominators’ stake should be distributed among the elected validators as evenly as possible, BUT still respect the nominators’ preferences. The end result, the election heuristic, should promote two key features, fair representation and security. 

**Fair Representation**

 In the late 19th century, Swedish mathematician Lars Edvard Phragmén proposed a method for electing members to his country’s parliament. He noticed that the election methods at the time tended to give all the seats to the most popular political party; in contrast, his new method ensured that the number of seats assigned to each party were proportional to the votes given to them, so it gave more representation to minorities. The property achieved by his method is formally known as **proportional justified representation**, and is very fitting for the NPoS election because it ensures that any pool of nodes is neither over-represented nor under-represented by the elected validators, proportional to their stake. NPoS builds on top of Phragmén’s suggested method and ensure this property in every election.

The illustration represents a typical input to the election process, with nominators on the left having different amounts of stake, and connected by lines to those validator candidates on the right that they trust \(for simplicity, validators have no stake of their own in this example, though they will in a real scenario\).

![](../.gitbook/assets/image%20%282%29.png)

 Suppose we need to elect n=4 validators. The fair representation property roughly translates to the rule that any nominator holding at least one n-th of the total stake is guaranteed to have at least one of their trusted validators elected. As the total stake is 40 EDG and a fourth of it is 10 EDG, the first two nominators are guaranteed to be represented by a validator. In the image below we see three possible election results: one that violates the fair representation property and two that achieve it.

![](../.gitbook/assets/image%20%281%29.png)

**Security**

If a nominator gets two or more of its trusted validators elected, we need to distribute **t**heir stake among them, in such a way that the validators’ backings are as balanced as possible. Recall that we want to make it as difficult as possible for an adversarial pool to get a validator elected, and they can achieve this only if they get a high enough backing. Therefore, we equate the level of security of an election result to _the minimum amount of backing of any elected validator_. For the last two election results with fair representation, we provide stake distributions which show that they achieve security levels of 6 and 9 respectively.

The election result on the right achieves a higher security level, and clearly does a better job at splitting the nominators’ stake into validators’ backings of roughly equal size. The goal of the NPoS election process is thus to provide a result that achieves fair representation and a security level that is as high as possible. This gives rise to a rather challenging optimization problem \(it is [NP-complete](https://www.britannica.com/science/NP-complete-problem)\), for which we have developed fast approximate heuristics with strong guarantees on security and scalability.

 To learn more about the operations side of the problem of electing validators in NPoS, view Web3 Foundation Research [technical overview.](https://research.web3.foundation/en/latest/polkadot/NPoS/1.%20Overview.html)
