# Creating an Account

There are currently two ways to generate an account in Edgeware. 

{% hint style="info" %}
**If you generated an account during the lockdrop period,** you need to regenerate your public address from your secret phrase or seed. At this time, the only way to do this is through a command line tool. 
{% endhint %}

{% page-ref page="../../validation-nodes/regenerating-keys-with-edgeware-network-id.md" %}

## Create an Edgeware Account

{% tabs %}
{% tab title="Subkey \(Command Line\)" %}
Subkey is a command line program that provides the most secure way to generate keypairs, but requires a firm understanding of command line tools and dependencies. If you are not technically strong here, consider using the Polkadot.js Browser Extension on Tab 2. 

After installing Subkey successfully, run:

```text
subkey -n edgeware generate
```

You should see an output something like below- **save all of this information somewhere secure you will not be able to recover your account if you lose your phrase or seed.**

```text
Secret phrase `favorite liar zebra assume hurt cage any damp inherit rescue delay panic` is account:
  Secret seed: 0x235c69907d33b85f27bd78e73ff5d0c67bd4894515cc30c77f4391859bc1a3f2
  Public key (hex): 0x6ce96ae5c300096b09dbd4567b0574f6a1281ae0e5cfe4f6b0233d1821f6206b
  Address (SS58): 5EXWNJuoProc7apm1JS8m9RTqV3vVwR9dCg6sQVpKnoHtJ68
```

{% hint style="info" %}
If you previously generated an account without the `-n edgeware` flag, you need to derive the  correct `Address` from your previous  `secret phrase` or`secret seed.`

You can use `subkey -n edgeware inspect "YOUR SECRET PHRASE HERE"` to obtain the network-ID inclusive Address \(SS58\)
{% endhint %}
{% endtab %}

{% tab title="Polkadot.js Browser Extension" %}
First, [Install Polkadot.Js](https://github.com/polkadot-js/extension) \(Scroll to bottom for links\)

Click the Orange P symbol in your extensions

Click "I want to create a new account with a new seed." 

![](../../.gitbook/assets/screen-shot-2020-02-06-at-5.37.08-pm.png)

{% hint style="info" %}
Store your mnemonic seed somewhere securely. You will need it to maintain access to your account.
{% endhint %}

Next, enter in a password for your account. **You should also store this securely.** 

Then click 'Add the account with the generated seed.'  
   
**Your new account should display in the list of accounts now and is ready for use.**
{% endtab %}
{% endtabs %}

## **What now?**

**Next**, consider connecting your account to [Commonwealth.im](http://Commonwealth.im) to access chain governance tools and community discussion, and also explore wallets to manage your EDG. You will need to sign a transaction from your account to do so, which will also require either the Polkadot.js tool or the Subkey program. 



{% page-ref page="../ecosystem/wallets-and-account-managers.md" %}

