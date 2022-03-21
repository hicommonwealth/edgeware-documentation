# Consensus

The following resources on nPoS are gratefully utilized and edited from Research at W3F - [https://research.web3.foundation/en/latest/polkadot/NPoS/index.html](https://research.web3.foundation/en/latest/polkadot/NPoS/index.html)

Edgeware uses nominated proof-of-stake \(NPoS\), a relatively new type of scheme used to select the validators who are allowed to participate in the consensus protocol. We also explain the peculiar way in which validators get elected.

## The NPoS scheme

This nominator-validator arrangement gives strong security guarantees. It allows for the system to select validators with massive amounts of aggregate stake — much higher than any single party’s EDG holdings — and eliminate candidates with low stake. In fact, at any given moment we expect there to be a considerable fraction of all the EDG supply be staked in NPoS. This makes it very difficult for an adversarial entity to get validators elected \(as they need to build a fair amount of **reputation** to get the required backing from nominators\) and also very costly to attack the system if they do get elected \(because any attack will result in large amounts of EDG being slashed.

{% hint style="info" %}
"Slashing" is the loss or taking of some staked EDG and transferring it to the Edgeware Treasury.
{% endhint %}

The NPoS scheme is much more efficient than proof-of-work \(PoW\) and faster than standard proof-of-stake \(PoS\). Networks with deterministic finality must have a limited validator set \(the size can be changed with governance\). NPoS allows for virtually all EDG holders to continuously participate, thus maintaining high levels of security by putting more value at stake and allowing more people to earn a yield based on their holdings.

{% hint style="info" %}
Through nomination, all EDG holders, not merely technically-capable validators, can participate in securing the network and benefitting from rewards.
{% endhint %}

