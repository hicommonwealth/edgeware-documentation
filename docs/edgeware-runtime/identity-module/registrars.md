# Registrars



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

