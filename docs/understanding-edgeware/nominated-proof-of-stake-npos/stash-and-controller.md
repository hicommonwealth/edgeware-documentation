---
description: 'https://wiki.polkadot.network/docs/en/learn-staking'
---

# Stash and Controller

### Accounts

There are two different accounts for managing your funds: `Stash` and `Controller`.

![staking](https://wiki.polkadot.network/docs/assets/NPoS/staking-keys_stash_controller.png)

* **Stash:** This account holds funds bonded for staking, but delegates some functions to a Controller. As a result, you may actively participate with a Stash key kept in a cold wallet, meaning it stays offline all the time. You can also designate a Proxy account to vote in [governance](https://wiki.polkadot.network/docs/en/learn-governance) proposals.
* **Controller** This account acts on behalf of the Stash account, signalling decisions about nominating and validating. It set preferences like payout account and commission. If you are a validator, it also sets your [session keys](https://wiki.polkadot.network/docs/en/learn-keys#session-keys). It only needs enough funds to pay transaction fees.

We designed this hierarchy of separate key types so that validator operators and nominators can protect themselves much better than in systems with only one key. As a rule, you lose security anytime you use one key for multiple roles, or even if you use keys related by derivation. You should never use any account key for a "hot" session key in particular.

Controller and Stash account keys can be either sr25519 or ed25519. For more on how keys are used in Substrate and the cryptography behind it [see here](https://wiki.polkadot.network/docs/en/learn-keys).

For more on how keys are used in Substrate and the cryptography behind it [see here](https://wiki.polkadot.network/docs/en/learn-keys).

