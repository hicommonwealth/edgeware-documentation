# Registrars



### Registrars

Registrars can set a fee for their services and limit their attestation to certain fields. For example, a registrar could charge 1 DOT to verify one's legal name, email, and GPG key. When a user requests judgement, they will pay this fee to the registrar who provides the judgement on those claims. Users set a maximum fee they are willing to pay and only registrars below this amount would provide judgement.

#### Becoming a registrar

To become a registrar, submit a pre-image and proposal into Democracy, then wait for people to vote on it. For best results, write a post about your identity and intentions beforehand, and once the proposal is in the queue ask people to second it so that it gets ahead in the referendum queue.

Here's how to submit a proposal to become a registrar:

Go to the Democracy tab, select "Submit preimage", and input the information for this motion - notably which account you're nominating to be a registrar in the `identity.setRegistrar` function.

![Setting a registrar](https://wiki.polkadot.network/img/identity/12.jpg)

Copy the preimage hash. In the above image, that's `0x90a1b2f648fc4eaff4f236b9af9ead77c89ecac953225c5fafb069d27b7131b7`. Submit the preimage by signing a transaction.

Next, select "Submit Proposal" and enter the previously copied preimage hash. The `locked balance` field needs to be at least 10 KSM. You can find out the minimum by querying the chain state under [Chain State](https://polkadot.js.org/apps/#/chainstate) -&gt; Constants -&gt; democracy -&gt; minimumDeposit.

![Submitting a proposal](https://wiki.polkadot.network/img/identity/13.jpg)

At this point, DOT holders can second the motion. With enough seconds, the motion will become a referendum which is then voted on. If it passes, users will be able to request judgement from this registrar.

### 

### Sub Accounts

Users can also link accounts by setting "sub accounts", each with its own identity, under a primary account. The system reserves a bond for each sub account. An example of how you might use this would be a validation company running multiple validators. A single entity, "My Staking Company", could register multiple sub accounts that represent the [Stash accounts](https://wiki.polkadot.network/docs/en/learn-keys) of each of their validators.

An account can have a maximum of 100 sub-accounts.

To register a sub-account on an existing account, you must currently use the [Extrinsics UI](https://polkadot.js.org/apps/#/extrinsics). There, select the identity pallet, then `setSubs` as the function to use. Click "Add Item" for every child account you want to add to the parent sender account. The value to put into the Data field of each parent is the optional name of the sub-account. If omitted, the sub-account will inherit the parent's name and be displayed as `parent/parent` instead of `parent/child`.

![Sub account setup](https://wiki.polkadot.network/img/identity/06.jpg)

Note that a deposit of 2.5KSM is required for every sub-account.

### Clearing and Killing

**Clearing:** Users can clear their identity information and have their deposit returned. Clearing an identity also clears all sub accounts and returns their deposits.

![Clearing an identity](https://wiki.polkadot.network/img/identity/clear.gif)

Clearing is done through the [Extrinsics UI](https://polkadot.js.org/apps/#/extrinsics).

**Killing:** The Council can kill an identity that it deems erroneous. This results in a slash of the deposit._Last updated on 1/31/2020 by Bruno Škvorc_[← GOVERNANCE](https://wiki.polkadot.network/docs/en/learn-governance)[BRIDGES →](https://wiki.polkadot.network/docs/en/learn-bridges)

* [Setting an Identity](https://wiki.polkadot.network/docs/en/learn-identity#setting-an-identity)
  * [Format Caveat](https://wiki.polkadot.network/docs/en/learn-identity#format-caveat)
* [Registrars](https://wiki.polkadot.network/docs/en/learn-identity#registrars)
  * [Becoming a registrar](https://wiki.polkadot.network/docs/en/learn-identity#becoming-a-registrar)
* [Judgements](https://wiki.polkadot.network/docs/en/learn-identity#judgements)
* [Sub Accounts](https://wiki.polkadot.network/docs/en/learn-identity#sub-accounts)
* 
