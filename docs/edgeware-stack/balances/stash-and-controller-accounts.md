# Staking Accounts: Stash and Controller

For Edgeware and many other PoS smart contract platforms, staking is the action that ensures the economic security of the blockchain. Users stake their tokens to a validator, who creates new blocks. For this effort, validators and nominators earn more tokens in the form of fees and inflationary rewards.

To participate in staking in Edgeware, a user is required to create and set multiple accounts for staking funds: `Stash` and `Controller`. This allows a user to separately manage their tokens in cold storage for the `Stash` account, and a `controller` account.

![staking](https://wiki.polkadot.network/docs/assets/NPoS/staking-keys_stash_controller.png)

* **Stash:** This account holds funds bonded for staking, but delegates some functions to a Controller. As a result, you may actively participate with a Stash key kept in a cold wallet, meaning it stays offline all the time. You can also designate a Proxy account to vote in [governance](https://wiki.polkadot.network/docs/en/learn-governance) proposals.
* **Controller** This account acts on behalf of the Stash account, signaling decisions about nominating and validating. It set preferences like payout account and commission. If you are a validator, it also sets your [session keys](https://wiki.polkadot.network/docs/en/learn-keys#session-keys). It only needs enough funds to pay transaction fees.

We designed this hierarchy of separate key types so that validator operators and nominators can protect themselves much better than in systems with only one key. As a rule, you lose security anytime you use one key for multiple roles, or even if you use keys related by derivation. You should never use any account key for a "hot" session key in particular.

For Edgeware, and specifically for Session Keys and validation, we use the ed25519 cryptographic curve. Controller and Stash account key are recommended to be in this format also. For more on how keys are used in Substrate and the cryptography behind it [see here](https://wiki.polkadot.network/docs/en/learn-keys).

```text
-> SessionKeys {
    SessionKeys {
        grandpa: ed25519_keyring.to_owned().public().into(),
        aura: ed25519_keyring.to_owned().public().into(),
        im_online: ed25519_keyring.to_owned().public().into(),
        authority_discovery: sr25519_keyring.to_owned().public().into(),
```

For more on how keys are used in Substrate and the cryptography behind it [see here](https://wiki.polkadot.network/docs/en/learn-keys).

Credit:[ https://wiki.polkadot.network/docs/en/learn-staking](https://wiki.polkadot.network/docs/en/learn-staking)

