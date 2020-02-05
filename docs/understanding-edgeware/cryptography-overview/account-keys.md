---
description: 'https://wiki.polkadot.network/docs/en/learn-keys'
---

# Account Keys

Public and private keys are an important aspect of most crypto-systems and an essential component that enables blockchains like Edgeware to exist.

### Account Keys

Account keys are keys that are meant to control funds. They can be either:

* The vanilla `ed25519` implementation using Schnorr signatures.
* The Schnorrkel/Ristretto `sr25519` variant using Schnorr signatures.

There are no differences in security between `ed25519` and `sr25519` for simple signatures.

We expect `ed25519` to be much better supported by commercial HSMs for the foreseeable future.

At the same time, `sr25519` makes implementing more complex protocols safer. In particular, `sr25519` comes with safer version of many protocols like HDKD common in the Bitcoin and Ethereum ecosystem.

#### "Controller" and "Stash" Keys

When we talk about "controller" and "stash" keys, we usually talk about them in the context of running a validator or nominating DOTs, but they are useful concepts for all users to know. Both keys are types of account keys. They are distinguished by their intended use, not by an underlying cryptographic difference. All the info mentioned in the parent section applies to these keys. When creating new controller or stash keys, all cryptography supported by account keys are an available option.

The controller key is a semi-online key that will be in the direct control of a user, and used to submit manual extrinsics. For validators or nominators, this means that the controller key will be used to start or stop validating or nominating. Controller keys should hold some DOTs to pay for fees, but they should not be used to hold huge amounts or life savings. Since they will be exposed to the internet with relative frequency, they should be treated carefully and occasionally replaced with new ones.

The stash key is a key that will, in most cases, be a cold wallet, existing on a piece of paper in a safe or protected by layers of hardware security. It should rarely, if ever, be exposed to the internet or used to submit extrinsics. The stash key is intended to hold a large amount of funds. It should be thought of as a saving's account at a bank, which ideally is only ever touched in urgent conditions. Or, perhaps a more apt metaphor is to think of it as buried treasure, hidden on some random island and only known by the pirate who originally hid it.

Since the stash key is kept offline, it must be set to have its funds bonded to a particular controller. For non-spending actions, the controller has the funds of the stash behind it. For example, in nominating, staking, or voting, the controller can indicate its preference with the weight of the stash. It will never be able to actually move or claim the funds in the stash key. However, if someone does obtain your controller key, they could use it for slashable behavior, so you should still protect it and change it regularly.

### Session Keys

Session keys are hot keys that be must kept online by a validator to perform network operations. Session keys are typically generated in the client, although they don't have to be. They are _not_ meant to control funds and should only be used for their intended purpose. They can be changed regularly; your controller only need create a certificate by signing a session public key and broadcast this certificate via an extrinsic.

Edgeware uses four session keys:

* GRANDPA: ed25519
* BABE: sr25519
* I'm Online: sr25519
* Parachain: sr25519

BABE requires keys suitable for use in a [Verifiable Random Function](https://wiki.polkadot.network/docs/en/learn-randomness#vrfs) as well as for digital signatures. Sr25519 keys have both capabilities and so are used for BABE.

In the future, we plan to use a BLS key for GRANDPA because it allows for more efficient signature aggregation.

