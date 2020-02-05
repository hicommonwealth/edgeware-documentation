# Staking in Edgeware

#### Intro

Edgeware uses NPoS \(Nominated Proof-of-Stake\) as its mechanism for selecting the validator set. It is designed with the roles of **validators** and **nominators**, to maximize chain security. Actors who are interested in maintaining the network can run a validator node. At genesis, Polkadot will have a limited amount of slots available for these validators, but this number can be altered through governance actions.

The system encourages EDG holders to participate as nominators. Nominators may back up to 16 validators as trusted validator candidates.

{% hint style="info" %}
Validators assume the role of producing new blocks in BABE, validating blocks, and guaranteeing finality. Nominators can choose to back select validators with their stake.
{% endhint %}

The staking system pays out rewards equally to all validators. Distribution of the rewards are pro-rata to all stakers after the validator payment is deducted. In this way, the network incents the nomination of lower-staked validators to create an equally-staked validator set.



