# Nominating

Any potential validators can indicate their intention to be a validator candidate. Their candidacies are made public to all nominators, and a nominator in turn submits a list of any number of candidates that it supports.

There are no particular requirements for a EDG holder to become a nominator, though we expect each nominator to carefully track the performance and reputation of validators. This guide will cover how to nominate validators in the Edgeware ecosystem.

Once nominated, you will see your nominations as 'Waiting nominations' which will change to 'Active nominations' after an era\(6 hours of period\).

For all the nominations older than an era\(6 hours\), the NPoS election mechanism takes the nominators and their associated votes as input, and outputs a set of validators of the required size, that maximizes the stake backing of any validator, and that makes the stakes backing validators as evenly distributed as possible.

Based on [Sequential Phragmén election algorithm](https://wiki.polkadot.network/docs/en/learn-phragmen) your stake gets dispersed in different proportions to any subset or all of the validators your choose.

The objectives of this election mechanism are to maximize the security of the network, and achieve fair representation of the nominators. If you want to know more about how NPoS works \(e.g. election, running time complexity, etc.\), please read [here](http://research.web3.foundation/en/latest/polkadot/NPoS/).

## Nominate EDG to a Validator

## See Your Nominated Amounts per Validator

{% hint style="info" %}
Nominating a Validator means that you delegate your EDG to be used for their validation purposes, and exposes you to the risk that the Validator may 'misbehave' according to the network, resulting in theirs AND your nominated EDG 'slashed,' or taken by the system as a disincentive to misbehave. Nominate responsibly.
{% endhint %}

{% tabs %}
{% tab title="Using the Polkadot.js UI \(Polkadot Apps\)" %}
### Step 1: Bond your tokens <a id="step-1-bond-your-tokens"></a>

**Prerequisites:**

* Have some EDG that you want to bond & stake in an account - we will call this the "**Stash**."
* Send only 5-10 EDG to another account that will control the nomination, we'll call this account the "**Controller.**" It will be used to pay the transaction fees, _without funds to pay fees, the nomination transaction will fail._ The stash and controller are recommended to keep separate for additional security. However, one can use the same\(single\) account as a stash as well as a controller without compromising any functionality.
* Research and select Validators to nominate. See link below for Validator list and details.

On the [Polkadot Apps UI](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fmainnet4.edgewa.re#/) navigate to the "Staking" option under "Network" tab.

{% hint style="info" %}
Ensure you are connected to Edgeware network on the Polkadot Apps UI, instead of Polkadot or any other Substrate network. \(Current network name can be found on the top-left corner.\)
{% endhint %}

The "Staking Overview" subsection will show you all the active validators and their information - points \(reliability\), earnings, identities, etc. The "Waiting" subsection lists all pending validators that need more nominations to enter the active validator set.

The "Account Actions" subsection allows you to stake and nominate and the "Validator Stats" screen will show you some interesting in-depth graphs about a selected validator.

The "Payouts" subsection allows you to claim rewards from staking.

The "Targets" subsection will help you estimate your earnings and this is where you can also pick favorite validators and nominate selected ones conveniently.

The "Waiting" subsection lists all pending validators that are awaiting more nominations to enter the active validator set. Validators will stay in the waiting queue until they have enough EDG backing them \(as allocated through the [Phragmén election mechanism](https://wiki.polkadot.network/docs/en/learn-phragmen)\). It is also possible that a validator can remain in the queue for a very long time if they never get enough backing.

The "Validator Stats" subsection allows you to query a validator's stash address and see historical charts on era points, elected stake, rewards, and slashes.

Pick "Account Actions", then click the "+ Stash" option you will find on right hand side.

![Bonding](https://raw.githubusercontent.com/Edgeware-Network/edgeware-documentation/master/docs/edgeware-runtime/staking/assets/images/nominating_1.jpg)

You will see a modal window that looks like the above.

Note: **Unbonding Duration**  
After unbonding, there is a period of 14 days which must pass before you can make those EDGs transferable.

Select a "value bonded" that is **less** than the total amount of EDG you have, so you have some left over to pay transaction fees. Be mindful of the reaping threshold - the amount that must remain in an account lest it be burned. That amount is 0.001 in Edgeware, so it's recommended to keep at least 0.001 EDG in your account to be on the safe side.

{% hint style="info" %}
**Parameter Note:** The Reaping Threshold, or the minimum number of EDG to maintain an account, is currently set to 0.001 EDG \(10\_000\_000\_000\_000 units.\)
{% endhint %}

Choose whatever payment destination sounds good to you. If you're unsure choose "Stash account \(increase amount at stake\)" which will yield compounding effect.

![Bonded](https://raw.githubusercontent.com/Edgeware-Network/edgeware-documentation/master/docs/edgeware-runtime/staking/assets/images/nominating_2.jpg)

### Step 2: Nominate a validator

You are now bonded. Being bonded means your tokens are locked and **could be** [**slashed**](https://wiki.polkadot.network/docs/en/learn-staking#slashing) **if the validators you nominate misbehave**. All bonded funds can now be distributed to up to 16 validators. Be careful about the validators you choose since you will be slashed if your validator commits an offense.

In the "Account actions" sub-tab you will find "Nominate" option corresponding to your stash\(the account you've bonded\) and upon clicking you will be presented with another popup asking you to select the intended validators, alternatively you can enter the validating address\(es\) of the validator\(s\) you wish to nominate.

![Nominating validators](https://raw.githubusercontent.com/Edgeware-Network/edgeware-documentation/master/docs/edgeware-runtime/staking/assets/images/nominating_3.jpg)

{% hint style="info" %}
Is your Nominate or Send button greyed out or not visible? Incase your are using the Polkadot JS extension, check your extension settings to ensure you have set the default network to Edgeware. Also make sure that you have both stash and controller accounts imported.
{% endhint %}

![Nominated](https://raw.githubusercontent.com/Edgeware-Network/edgeware-documentation/master/docs/edgeware-runtime/staking/assets/images/nominating_4.jpg)

Select them, confirm the transaction, and you're done - you are now nominating. Your stash will start generating staking rewards within an era \(6 hours\). You will notice your balance increasing whenever a validator or any nominator corresponding to it claims a payout \(on behalf of every corresponding nominators\).
{% endtab %}

{% tab title="using Subkey to Sign Transactions Securely" %}
Coming soon.
{% endtab %}
{% endtabs %}

## Stop Being a Nominator \(unbond\)

At some point, you might decide to stop nominating one or more validators. You can always change who you're nominating, but you cannot withdraw your tokens unless you unbond them. The following guide describes how to stop nominating and then unbond to retrieve your EDGs.

On the [Polkadot Apps UI](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fmainnet4.edgewa.re#/), **connect to the Edgeware endpoint**, navigate to the "Staking" option under "Network" tab.

On this tab click on the "Account actions" sub-tab at the top of the screen.

{% hint style="info" %}
**Parameter Note:** Unbonding Time: 14 days  
You may stop nominating at any time, but **withdrawing unbonded will fail if 14 days haven't passed since you bonded.**
{% endhint %}

#### Step 1: Stop Nominating

Here, click "Stop" option corresponding to your stash which will prompt you to enter sign an extrinsic via your Controller account.

#### Step 2: Unbonding an amount

To unbond the amount, click the 3-dot menu corresponding to your stash from which you want to unbond EDGs and select "Unbond funds". Your can then enter intended amount to unbond and select "Unbond" option which will prompt a transaction/extrinsic.

![Unbonding](https://raw.githubusercontent.com/Edgeware-Network/edgeware-documentation/master/docs/edgeware-runtime/staking/assets/images/nominating_5.png)

After you confirm this transaction, your EDGs will remain _bonded_ until the unbonding period of 14 days passes. Your balance will show as "unbonding" with an indicator of how many more blocks remain until the amount is fully unlocked.

![Unbonding duration](https://raw.githubusercontent.com/Edgeware-Network/edgeware-documentation/master/docs/edgeware-runtime/staking/assets/images/nominating_6.png)

Once the 14 days of unbonding period passes, you will have to issue another\(final\) transaction/extrinsic: withdrawUnbonded. You can prompt this transaction/extrinsic by simply clicking on the lock symbol corresponding to your stash in "Account actions" sub-tab. ![WithdrawUnbonded](https://raw.githubusercontent.com/Edgeware-Network/edgeware-documentation/master/docs/edgeware-runtime/staking/assets/images/nominating_7_1.jpg)

Then, your transferrable balance will increase by the amount of tokens you've just fully unbonded.

