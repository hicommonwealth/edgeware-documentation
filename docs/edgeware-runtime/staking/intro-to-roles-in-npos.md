---
description: 'https://wiki.polkadot.network/docs/en/learn-staking#validators-and-nominators'
---

# Intro to Roles in NPoS

## Validators and Nominators <a id="validators-and-nominators"></a>

Since validator slots will be limited, most of those who wish to stake their EDG and contribute economic security to the network will be nominators. **Validators** do most of the heavy lifting: they produce new block candidates, vote and come to consensus, validate the chain's blocks.

**Nominators,** on the other hand, do not need to do anything once they have bonded their EDG. The experience of the nominator is similar to "set it and forget it," while the validator will be doing active service for the network by performing the critical operations.

{% hint style="info" %}
As the more active participant, the validator has certain privileges regarding the payout of the staking mechanism and will be able to declare its own allocation before the share is divided to nominators.
{% endhint %}

### Validators

A couple of times per day, the system elects a group of entities called **validators**, who in the next few hours will play a key role in highly sensitive protocols such as block production block finality. Their job is demanding as they need to run costly operations, ensure high communication responsiveness, and build a long-term reputation of reliability.

They also must stake their EDG, Edgeware’s native token, as a guarantee of good behavior, and this stake gets slashed whenever they deviate from their protocol. In contrast, they get paid well when they play by the rules. Any node that is up to the task can publicly offer itself as a validator candidate. However, for operational reasons only a limited number of validators can be elected, expected to be hundreds or thousands.

{% hint style="info" %}
**Parameter Note:** Edgeware initially allows 60 Validator slots, but this number can change through governance actions.
{% endhint %}

{% page-ref page="slashing-consequences.md" %}

### Nominators

The system also encourages **any** EDG holder to participate as a **nominator**. A nominator publishes a list of validator candidates that they trust, and puts down an amount of EDG at stake to support them with. If some of these candidates are elected as validators, she shares with them the payments, or the sanctions, on a per-staked-EDG basis.

Unlike validators, an _unlimited_ number of parties can participate as nominators. As long as a nominator is diligent in their choice and only supports validator candidates with good security practices, the role carries low risk and provides a continuous source of revenue.

