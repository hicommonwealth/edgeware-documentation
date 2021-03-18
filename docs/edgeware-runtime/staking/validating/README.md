# Validating

## The Validator Election Process[¶]() <a id="the-election-process"></a>

You can look at our quick start guide to start participating in validating

How to elect the validators, given the nominators’ votes? Unlike other PoS-based projects where validators are weighted by stake, NPoS gives elected validators equal voting power in the consensus protocol.

To achieve proportional representation regardless of that fact, the total pool of their nominators’ stake should be distributed among the elected validators as evenly as possible, BUT still respect the nominators’ preferences. The end result, the election heuristic, should promote two key features, fair representation and security.

**Fair Representation**

In the late 19th century, Swedish mathematician Lars Edvard Phragmén proposed a method for electing members to his country’s parliament. He noticed that the election methods at the time tended to give all the seats to the most popular political party; in contrast, his new method ensured that the number of seats assigned to each party were proportional to the votes given to them, so it gave more representation to minorities. The property achieved by his method is formally known as **proportional justified representation**, and is very fitting for the NPoS election because it ensures that any pool of nodes is neither over-represented nor under-represented by the elected validators, proportional to their stake. NPoS builds on top of Phragmén’s suggested method and ensure this property in every election.

The illustration represents a typical input to the election process, with nominators on the left having different amounts of stake, and connected by lines to those validator candidates on the right that they trust \(for simplicity, validators have no stake of their own in this example, though they will in a real scenario\).

![](../../../.gitbook/assets/image%20%286%29%20%282%29%20%282%29%20%281%29.png)

Suppose we need to elect n=4 validators. The fair representation property roughly translates to the rule that any nominator holding at least one n-th of the total stake is guaranteed to have at least one of their trusted validators elected. As the total stake is 40 EDG and a fourth of it is 10 EDG, the first two nominators are guaranteed to be represented by a validator. In the image below we see three possible election results: one that violates the fair representation property and two that achieve it.

![](../../../.gitbook/assets/image%20%282%29%20%281%29%20%281%29.png)

**Security**

If a nominator gets two or more of its trusted validators elected, we need to distribute **t**heir stake among them, in such a way that the validators’ backings are as balanced as possible. Recall that we want to make it as difficult as possible for an adversarial pool to get a validator elected, and they can achieve this only if they get a high enough backing. Therefore, we equate the level of security of an election result to _the minimum amount of backing of any elected validator_. For the last two election results with fair representation, we provide stake distributions which show that they achieve security levels of 6 and 9 respectively.

The election result on the right achieves a higher security level, and clearly does a better job at splitting the nominators’ stake into validators’ backings of roughly equal size. The goal of the NPoS election process is thus to provide a result that achieves fair representation and a security level that is as high as possible. This gives rise to a rather challenging optimization problem \(it is [NP-complete](https://www.britannica.com/science/NP-complete-problem)\), for which we have developed fast approximate heuristics with strong guarantees on security and scalability.

To learn more about the operations side of the problem of electing validators in NPoS, view Web3 Foundation Research [technical overview.](https://research.web3.foundation/en/latest/polkadot/NPoS/1.%20Overview.html)

