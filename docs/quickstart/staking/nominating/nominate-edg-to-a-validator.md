# Nominate EDG to a Validator

This guide will cover how to nominate validators in the Edgeware ecosystem. 

{% hint style="info" %}
Nominating a Validator means that you delegate your EDG to be used for their validation purposes, and exposes you to the risk that the Validator may 'misbehave' according to the network, resulting in theirs AND your nominated EDG 'slashed,' or taken by the system as a disincentive to misbehave. Nominate responsibly.
{% endhint %}

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



Click on "Nominate" on an account you've bonded and you may  be presented with another popup asking you to select some validators, otherwise enter the validating address of the validator you wish to nominate.

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



###  <a id="step-1-bond-your-tokens"></a>



