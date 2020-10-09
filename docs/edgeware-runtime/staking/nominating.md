# Nominating

Any potential validators can indicate their intention to be a validator candidate. Their candidacies are made public to all nominators, and a nominator in turn submits a list of any number of candidates that it supports.

## Nominate EDG to a Validator

In the next epoch \(lasting several hours\), a certain number of validators having the most EDG backing get elected and become active. There are no particular requirements for a EDG holder to become a nominator, though we expect each nominator to carefully track the performance and reputation of validators.

This guide will cover how to nominate validators in the Edgeware ecosystem.

Once the nomination period ends, the NPoS election mechanism takes the nominators and their associated votes as input, and outputs a set of validators of the required size, that maximizes the stake backing of any validator, and that makes the stakes backing validators as evenly distributed as possible.

{% hint style="info" %}
Nominating a Validator means that you delegate your EDG to be used for their validation purposes, and exposes you to the risk that the Validator may 'misbehave' according to the network, resulting in theirs AND your nominated EDG 'slashed,' or taken by the system as a disincentive to misbehave. Nominate responsibly.
{% endhint %}

The objectives of this election mechanism are to maximize the security of the network, and achieve fair representation of the nominators. If you want to know more about how NPoS works \(e.g. election, running time complexity, etc.\), please read [here](http://research.web3.foundation/en/latest/polkadot/NPoS/).

{% tabs %}
{% tab title="Using the Polkadot.js UI" %}
### Step 1: Bond your tokens <a id="step-1-bond-your-tokens"></a>

**Prerequisites:**

* Have some EDG that you want to bond & stake in an account - we will call this the "**Stash**."
* Send only 5-10 EDG to another account that will control the nomination, we'll call this account the "**Controller.**" It will be used to pay the transaction fees, _without funds to pay fees, the nomination transaction will fail._ The stash and controller are separate for security.
* Research and select Validators to nominate. See link below for Validator list and details.

On the [Polkadot UI](https://polkadot.js.org/apps) navigate to the "Staking" tab.

{% hint style="info" %}
Ensure you are connected to Edgeware on the Polkadot UI, instead of Kusama or other Substrate networks.
{% endhint %}

The "Staking Overview" subsection will show you all the active validators and their information - points \(reliability\), earnings, identities, etc. The "Waiting" subsection lists all pending validators that need more nominations to enter the active validator set.

The "Returns" screen will help you estimate your earnings and this is where it's good to start picking favorites. The "Account Actions" subsection allows you to stake and nominate and the "Validator Stats" screen will show you some interesting in-depth graphs about a selected validator.

Pick "Account Actions", then click the blue "New Stake" button.

![Bonding](https://guide.kusama.network/en/latest/img/NPoS/nominate2.png)

You will see a modal window that looks like the above.

Note: **Unbonding Duration**  
Once you bond, a period of 7 days must pass before you can unbond tokens.

Select a "value bonded" that is **less** than the total amount of EDG you have, so you have some left over to pay transaction fees. Be mindful of the reaping threshold - the amount that must remain in an account lest it be burned. That amount is 0.001 in Edgeware, so it's recommended to keep at least 0.001 EDG in your account to be on the safe side.

{% hint style="info" %}
**Parameter Note:** The Reaping Threshold, or the minimum number of EDG to maintain an account, is currently set to 0.001 EDG \(10\_000\_000\_000\_000 units.\)
{% endhint %}

Choose whatever payment destination sounds good to you. If you're unsure choose "Stash account \(increase amount at stake\)".

### Step 2: Nominate a validator

You are now bonded. Being bonded means your tokens are locked and **could be** [**slashed**](https://wiki.polkadot.network/docs/en/learn-staking#slashing) **if the validators you nominate misbehave**. All bonded funds can now be distributed to up to 16 validators. Be careful about the validators you choose since you will be slashed if your validator commits an offense.

Click on "Nominate" on an account you've bonded and you may be presented with another popup asking you to select some validators, otherwise enter the validating address of the validator you wish to nominate.

{% hint style="info" %}
Is your Nominate or Send button greyed out? Check your settings in the popup to ensure you have the default network or Edgeware selected.
{% endhint %}

![Nominating validators](https://guide.kusama.network/en/latest/img/NPoS/nominate.png)

Select them, confirm the transaction, and you're done - you are now nominating. You should notice your balance increasing shortly.

### Step 3: Stop nominating

At some point, you might decide to stop nominating one or more validators. You can always change who you're nominating, but you cannot withdraw your tokens unless you unbond them.

{% hint style="info" %}
**Parameter Note:** Unbonding Time: 7 days  
You may stop nominating at any time, but **unbonding may fail if 7 days haven't passed since you bonded.**
{% endhint %}
{% endtab %}

{% tab title="using Subkey to Sign Transactions Securely" %}
Coming soon.
{% endtab %}
{% endtabs %}

## Nominate EDG to a Validator

## See Your Nominated Amounts per Validator

This guide will cover how to nominate validators in the Edgeware ecosystem.

To see the absolute values of how the Phragmen method allocates your nominated EDG, [using the Polkadot UI](https://polkadot.js.org/apps/#/explorer)

{% hint style="info" %}
Nominating a Validator means that you delegate your EDG to be used for their validation purposes, and exposes you to the risk that the Validator may 'misbehave' according to the network, resulting in theirs AND your nominated EDG 'slashed,' or taken by the system as a disincentive to misbehave. Nominate responsibly.
{% endhint %}

1. Click into Stacking Overview, 
2. Find the validator you nominated to, 
3. Click Other Stake 
4. Find your account ID in the list to see your stake towards this validator.
5. Repeat for as many validators as you want to examine.

{% tabs %}
{% tab title="Using the Polkadot.js UI" %}
### Step 1: Bond your tokens <a id="step-1-bond-your-tokens"></a>

**Prerequisites:**

* Have some EDG that you want to bond & stake in an account - we will call this the "**Stash**."
* Send only 5-10 EDG to another account that will control the nomination, we'll call this account the "**Controller.**" It will be used to pay the transaction fees, _without funds to pay fees, the nomination transaction will fail._ The stash and controller are separate for security.
* Research and select Validators to nominate. See link below for Validator list and details.

On the [Polkadot UI](https://polkadot.js.org/apps) navigate to the "Staking" tab.

{% hint style="info" %}
Ensure you are connected to Edgeware on the Polkadot UI, instead of Kusama or other Substrate networks.
{% endhint %}

The "Staking Overview" subsection will show you all the active validators and their information - points \(reliability\), earnings, identities, etc. The "Waiting" subsection lists all pending validators that need more nominations to enter the active validator set.

The "Returns" screen will help you estimate your earnings and this is where it's good to start picking favorites. The "Account Actions" subsection allows you to stake and nominate and the "Validator Stats" screen will show you some interesting in-depth graphs about a selected validator.

Pick "Account Actions", then click the blue "New Stake" button.

![Bonding](https://guide.kusama.network/en/latest/img/NPoS/nominate2.png)

You will see a modal window that looks like the above.

Note: **Unbonding Duration**  
Once you bond, a period of 7 days must pass before you can unbond tokens.

Select a "value bonded" that is **less** than the total amount of EDG you have, so you have some left over to pay transaction fees. Be mindful of the reaping threshold - the amount that must remain in an account lest it be burned. That amount is 0.001 in Edgeware, so it's recommended to keep at least 0.001 EDG in your account to be on the safe side.

{% hint style="info" %}
**Parameter Note:** The Reaping Threshold, or the minimum number of EDG to maintain an account, is currently set to 0.001 EDG \(10\_000\_000\_000\_000 units.\)
{% endhint %}

Choose whatever payment destination sounds good to you. If you're unsure choose "Stash account \(increase amount at stake\)".

### Step 2: Nominate a validator

You are now bonded. Being bonded means your tokens are locked and **could be** [**slashed**](https://wiki.polkadot.network/docs/en/learn-staking#slashing) **if the validators you nominate misbehave**. All bonded funds can now be distributed to up to 16 validators. Be careful about the validators you choose since you will be slashed if your validator commits an offense.

Click on "Nominate" on an account you've bonded and you may be presented with another popup asking you to select some validators, otherwise enter the validating address of the validator you wish to nominate.

{% hint style="info" %}
Is your Nominate or Send button greyed out? Check your settings in the popup to ensure you have the default network or Edgeware selected.
{% endhint %}

![Nominating validators](https://guide.kusama.network/en/latest/img/NPoS/nominate.png)

Select them, confirm the transaction, and you're done - you are now nominating. You should notice your balance increasing shortly.

### Step 3: Stop nominating

At some point, you might decide to stop nominating one or more validators. You can always change who you're nominating, but you cannot withdraw your tokens unless you unbond them.

{% hint style="info" %}
**Parameter Note:** Unbonding Time: 7 days  
You may stop nominating at any time, but **unbonding may fail if 7 days haven't passed since you bonded.**
{% endhint %}
{% endtab %}

{% tab title="using Subkey to Sign Transactions Securely" %}
Coming soon.
{% endtab %}
{% endtabs %}

![](../../.gitbook/assets/image%20%287%29%20%281%29.png)

## See Your Nominated Amounts per Validator

## Stop Being a Nominator \(unbond\)

To see the absolute values of how the Phragmen method allocates your nominated EDG, [using the Polkadot UI](https://polkadot.js.org/apps/#/explorer)

The following describes how to stop nominating and retrieve your tokens. Please note that all networks on which you can nominate have a delayed exit period, called the _unbonding period_, which serves as a cooldown. You will not be able to transfer your tokens before this period has elapsed.

1. Click into Stacking Overview, 
2. Find the validator you nominated to, 
3. Click Other Stake 
4. Find your account ID in the list to see your stake towards this validator.
5. Repeat for as many validators as you want to examine.

#### Step 1: Stop Nominating

## Stop Being a Nominator \(unbond\)

On the [Polkadot UI](https://polkadot.js.org/apps), **connect to the Edgeware endpoint**, navigate to the "Staking" tab.

The following describes how to stop nominating and retrieve your tokens. Please note that all networks on which you can nominate have a delayed exit period, called the _unbonding period_, which serves as a cooldown. You will not be able to transfer your tokens before this period has elapsed.

On this tab click on the "Account Actions" tab at the top of the screen.

#### Step 1: Stop Nominating

Here, click "Stop Nominating" on an account you're nominating with and would like to free the funds for.

On the [Polkadot UI](https://polkadot.js.org/apps), **connect to the Edgeware endpoint**, navigate to the "Staking" tab.

![Stop Nominating Button](https://wiki.polkadot.network/img/NPoS/unbond1.png)

On this tab click on the "Account Actions" tab at the top of the screen.

After you confirm this transaction, your tokens will remain _bonded_. This means they stay ready to be distributed among nominees again. To actually withdraw them, you need to unbond.

Here, click "Stop Nominating" on an account you're nominating with and would like to free the funds for.

#### Step 2: Unbonding an amount

![Stop Nominating Button](https://wiki.polkadot.network/img/NPoS/unbond1.png)

To unbond the amount, click the little gear icon next to the account you want to unbond money for, and select "Unbond funds".

After you confirm this transaction, your tokens will remain _bonded_. This means they stay ready to be distributed among nominees again. To actually withdraw them, you need to unbond.

![Unbonding](https://wiki.polkadot.network/img/NPoS/unbond2.png)

#### Step 2: Unbonding an amount

Select the amount you wish to unbond and click Unbond, then confirm the transaction.

To unbond the amount, click the little gear icon next to the account you want to unbond money for, and select "Unbond funds".

![Unbonding all](https://wiki.polkadot.network/img/NPoS/unbond3.png)

![Unbonding](https://wiki.polkadot.network/img/NPoS/unbond2.png)

If successful, your balance will show as "unbonding" with an indicator of how many more blocks remain until the amount is fully unlocked.

Select the amount you wish to unbond and click Unbond, then confirm the transaction.

**Unbonding Duration**  
Once you bond, a period of 7 days must pass before you can unbond tokens.

![Unbonding all](https://wiki.polkadot.network/img/NPoS/unbond3.png)

{% hint style="info" %}
**Parameter Note:** Unbonding Duration: 7 days. The length of time that must pass before you can unbond.
{% endhint %}

If successful, your balance will show as "unbonding" with an indicator of how many more blocks remain until the amount is fully unlocked.

![Unbonding duration](https://wiki.polkadot.network/img/NPoS/unbond4.png)

**Unbonding Duration**  
Once you bond, a period of 7 days must pass before you can unbond tokens.

This duration will vary depending on the network you're on.

{% hint style="info" %}
**Parameter Note:** Unbonding Duration: 7 days. The length of time that must pass before you can unbond.
{% endhint %}

Once this process is complete, you will have to issue another, final transaction: Withdraw Unbonded. Then, your transferrable balance will increase by the amount of tokens you've just fully unbonded.

![Unbonding duration](https://wiki.polkadot.network/img/NPoS/unbond4.png)

This duration will vary depending on the network you're on.

Once this process is complete, you will have to issue another, final transaction: Withdraw Unbonded. Then, your transferrable balance will increase by the amount of tokens you've just fully unbonded.

