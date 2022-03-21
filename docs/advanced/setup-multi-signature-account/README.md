# Setup Multi Signature Account

It is possible to create a multi-signature account in Substrate based chains like Edgeware. A multi-signature account is composed of one or more addresses and a threshold. The threshold defines how many signatories (participating addresses) need to agree on the submission of an extrinsic in order for the call to be successful.

For example, Alice, Bob, and Charlie set up a multi-sig with a threshold of 2. This means Alice and Bob can execute any call even if Charlie disagrees with it. Likewise, Charlie and Bob can execute any call without Alice. A threshold is typically a number smaller than the total number of members but can also be equal to it, which means they all have to be in agreement.

Multi-signature accounts have several uses:

* **securing your own stash**: use additional signatories as a 2FA mechanism to secure your funds. One signer can be on one computer, another can be on another, or in cold storage. This slows down your interactions with the chain, but is orders of magnitude more secure.
* **board decisions**: legal entities such as businesses and foundations use multi-sigs to collectively govern over the entity's treasury.
* **group participation in governance**: a multi-sig account can do everything a regular account can. A multi-sig account could be a council member in Kusama's governance, where a set of community members could vote as one entity.

**Multi-signature accounts cannot be modified after being created**. Changing the set of members or altering the threshold is not possible and instead requires termination of the current multi-sig and the creation of a new one. As such, multi-sig account addresses are **deterministic**, i.e. you can always calculate the address of a multi-sig just by knowing the members and the threshold, without the account existing yet. This means one can send tokens to an address that does not exist yet, and if the entities designated as the recipients come together in a new multi-sig under a matching threshold, they will immediately have access to these tokens.



## Resources

* [How to Create and Use Multisigs](https://www.youtube.com/watch?v=ZJLqszvhMyM\&list=PLOyWqupZ-WGuAuS00rK-pebTMAOxW41W8\&index=25\&ab_channel=Polkadot)
* [Learn more about Multi Signature accounts](https://wiki.polkadot.network/docs/en/learn-accounts#multi-signature-accounts)
* [Generate a Multisig Account from code](https://polkadot.js.org/docs/util-crypto/examples/create-multisig/)
