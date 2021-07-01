---
description: 'https://wiki.polkadot.network/docs/en/learn-identity'
---

# Identity

### Judgements

After a user injects their information on chain, they can request judgement from a registrar. Users declare a maximum fee that they are willing to pay for judgement, and registrars whose fee is below that amount can provide a judgement.

When a registrar provides judgement, they can select up to six levels of confidence in their attestation:

* Unknown: The default value, no judgement made yet.
* Reasonable: The data appears reasonable, but no in-depth checks \(e.g. formal KYC process\) were performed.
* Known Good: The registrar has certified that the information is correct.
* Out of Date: The information used to be good, but is now out of date.
* Low Quality: The information is low quality or imprecise, but can be fixed with an update.
* Erroneous: The information is erroneous and may indicate malicious intent.

A seventh state, "fee paid", is for when a user has requested judgement and it is in progress. Information that is in this state or "erroneous" is "sticky" and cannot be modified; it can only be removed by complete removal of the identity.

Registrars gain trust by performing proper due diligence and would presumably be replaced for issuing faulty judgements.

To be judged after submitting your identity information, go to the ["Extrinsics UI"](https://polkadot.js.org/apps/#/extrinsics) and select the `identity` pallet, then `requestJudgement`. For the `reg_index` put the index of the registrar you want to be judged by, and for the `max_fee` put the maximum you're willing to pay for these confirmations.

If you don't know which registrar to pick, first check the available registrars by going to ["Chain State UI"](https://wiki.polkadot.network/docs/en/learn-identity) and selecting `identity.registrars()` to get the full list.

![Showing all registrars](https://wiki.polkadot.network/img/identity/14.jpg)

The image above reveals two registrars:

* Registrar 0, FcxNWVy5RESDsErjwyZmPCW6Z8Y3fbfLzmou34YZTrbcraL charges 25 KSM per judgement
* Registrar 1, Fom9M5W6Kck1hNAiE2mDcZ67auUCiNTzLBUdQy4QnxHSxdn charges 5 KSM per judgement

To find out how to contact the registrar after the application for judgement or to learn who they are, we can check their identity by adding them to our Address Book. Their identity will be automatically loaded.

![Gav is a registrar](https://wiki.polkadot.network/img/identity/15.jpg)

Gavin Wood is registrar \#0.

![Chevdor is registrar \#1](https://wiki.polkadot.network/img/identity/16.jpg)

Chevdor is registrar \#1. We pick that one.

![Requesting judgement](https://wiki.polkadot.network/img/identity/08.jpg)

This will make your identity go from unjudged:

![An unjudged identity](https://wiki.polkadot.network/img/identity/07.jpg)

To "waiting":

![A pending identity](https://wiki.polkadot.network/img/identity/09.jpg)

At this point, direct contact with the registrar is required - the contact info is in their identity as shown above. Each registrar will have their own set of procedures to verify your identity and values, and only once you've satisfied their requirements will the process continue.

Once the registrar has confirmed the identity, a green checkmark should appear next to your account name with the appropriate confidence level:

![A confirmed identity](https://wiki.polkadot.network/img/identity/10.jpg)

_Note that changing even a single field's value after you've been verified will un-verify your account and you will need to start the judgement process anew. However, you can still change fields while the judgement is going on - it's up to the registrar to keep an eye on the changes._

## Clearing and Killing

**Clearing:** Users can clear their identity information and have their deposit returned. Clearing an identity also clears all sub accounts and returns their deposits.

{% hint style="info" %}
**Killing:** The Council can kill an identity that it deems erroneous. **This results in a slash of the deposit.**
{% endhint %}

![Clearing an identity](https://wiki.polkadot.network/img/identity/clear.gif)

Clearing is done through the [Extrinsics UI](https://polkadot.js.org/apps/#/extrinsics).

## Sub Accounts

Users can also link accounts by setting "sub accounts", each with its own identity, under a primary account. The system reserves a bond of 2 EDG for each sub account. An example of how you might use this would be a validation company running multiple validators. A single entity, "My Staking Company", could register multiple sub accounts that represent the [Stash accounts](https://wiki.polkadot.network/docs/en/learn-keys) of each of their validators.

{% hint style="info" %}
**Parameter Note:** The Sub Account Bond, the returnable fee charged for adding a sub-account, is 2 EDG per sub-account.
{% endhint %}

{% hint style="info" %}
**Parameter Note:** The Sub-account limit, the amount of sub-accounts an account may have, is 100.
{% endhint %}

To register a sub-account on an existing account, you must currently use the [Extrinsics UI](https://polkadot.js.org/apps/#/extrinsics). There, select the identity pallet, then `setSubs` as the function to use. Click "Add Item" for every child account you want to add to the parent sender account. The value to put into the Data field of each parent is the optional name of the sub-account. If omitted, the sub-account will inherit the parent's name and be displayed as `parent/parent` instead of `parent/child`.

![Sub account setup](https://wiki.polkadot.network/img/identity/06.jpg)

Note that a deposit is required for every sub-account.

### Registrars

Registrars can set a fee for their services and limit their attestation to certain fields. For example, a registrar could charge 1 EDG to verify one's legal name, email, and GPG key. When a user requests judgement, they will pay this fee to the registrar who provides the judgement on those claims. Users set a maximum fee they are willing to pay and only registrars below this amount would provide judgement.

#### Becoming a registrar

To become a registrar, submit a pre-image and proposal into Democracy, then wait for people to vote on it. For best results, write a post about your identity and intentions beforehand, and once the proposal is in the queue ask people to second it so that it gets ahead in the referendum queue.

Here's how to submit a proposal to become a registrar:

Go to the Democracy tab, select "Submit preimage", and input the information for this motion - notably which account you're nominating to be a registrar in the `identity.setRegistrar` function.

![Setting a registrar](https://wiki.polkadot.network/img/identity/12.jpg)

Copy the preimage hash. In the above image, that's `0x90a1b2f648fc4eaff4f236b9af9ead77c89ecac953225c5fafb069d27b7131b7`. Submit the preimage by signing a transaction.

Next, select "Submit Proposal" and enter the previously copied preimage hash. The `locked balance` field needs to be at least \[TO ADD\]. You can find out the minimum by querying the chain state under [Chain State](https://polkadot.js.org/apps/#/chainstate) -&gt; Constants -&gt; democracy -&gt; minimumDeposit.

![Submitting a proposal](https://wiki.polkadot.network/img/identity/13.jpg)

At this point, EDG holders can second the motion. With enough seconds, the motion will become a referendum which is then voted on. If it passes, users will be able to request judgement from this registrar.

## Ethereum Name Services

### Adding accounts to an ENS domain

> This tutorial is found on the [Polkadot wiki](https://wiki.polkadot.network/docs/en/ens) and references Kusama \(KSM\) and DOT for the examples. An updated version will be displayed when Edgeware is supported.

ENS \(Ethereum Name Service\) is a system of smart contracts on the Ethereum blockchain which allows users to claim domain names like `bruno.eth`. Supporting wallets can then allow senders to input ENS domains instead of long and unwieldy addresses. This prevents phishing, fraud, typos, and adds a layer of usability on top of the regular wallet user experience.

> Note: You will need an ENS name and an Ethereum account with some ether in it to follow along with this guide. To register an ENS name, visit the [ENS App](https://app.ens.domains/) or any number of subdomain registrars like [Nameth](https://nameth.io/). Note that if you're using an older ENS name, you should make sure you're using the [new resolver](https://medium.com/the-ethereum-name-service/ens-registry-migration-is-over-now-what-a-few-things-to-know-fb05f921872a). Visiting the ENS App will warn you about this if not. You will also need some way to use your Ethereum address - following this guide on a personal computer is recommended. Wallets like [Frame](https://frame.sh/) and [Metamask](identity.md) are safe and will make interacting with the Ethereum blockchain through your browser very easy.

Despite living on the Ethereum blockchain, the ENS system has multi-chain support. In this guide you'll go through the process of adding a KSM and DOT address to ENS. We cover both KSM and DOT to show two different approaches.

> Note: DOT can currently only be added using the Resolver method. KSM can be added through both methods described below.

This guide is also available in video format on [Youtube](https://www.youtube.com/watch?v=XKjZk-5_mQc).

#### Adding via the UI

The [ENS App](https://app.ens.domains/) allows an ENS domain owner to inspect all records bound to the domain, and to add new ones.

![](https://user-images.githubusercontent.com/32852637/116083672-e5f95900-a66a-11eb-9f58-1c363f056b12.png)

In the example above, the domain `bruno.eth` has an Ethereum and a Bitcoin address attached. Let's attach a KSM account. First, click the `[+]` icon in the Records tab.

![](https://user-images.githubusercontent.com/32852637/116084676-070e7980-a66c-11eb-8390-29c60879b29c.png)

Then, pick "Other Addresses", "KSM", and input the Kusama address:

![](https://user-images.githubusercontent.com/32852637/116084772-1e4d6700-a66c-11eb-9915-df76e5d30215.png)

After clicking Save, your Ethereum wallet will ask you to confirm a transaction. Once processed, the record will show up on the domain's page:

![](https://user-images.githubusercontent.com/32852637/116084852-345b2780-a66c-11eb-9189-479f04b4e235.png)

The same process applies to adding your DOT address.

Once the transaction is confirmed, your address will be bound to your ENS domain.

#### Wallet Support

There is no wallet support for ENS names for either KSM or DOT at this time, but the crypto accounting and portfolio application [Rotki](https://rotki.com/) does support KSM ENS resolution.

#### Relevant links

* [ENS docs](https://docs.ens.domains/)
* [ENS Multi-chain announcement](https://medium.com/the-ethereum-name-service/ens-launches-multi-coin-support-15-wallets-to-integrate-92518ab20599)
* [Address encoder](https://github.com/ensdomains/address-encoder)
* [Namehash calculator](https://swolfeyes.github.io/ethereum-namehash-calculator/)
* [Address to pubkey converter](https://www.shawntabrizi.com/substrate-js-utilities/)

