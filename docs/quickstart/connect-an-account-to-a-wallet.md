# Connect to a Wallet and Check Balance

Follow this guide to connect your Edgeware address to a wallet and get started on the network by first checking your balance. Please note, if you received your EDG from an exchange, you won't need to follow the step of "converting a Lockdrop Address" in this guide and instead can directly connect your account in step two.

## Convert a Lockdrop Address to the New Format

Lockdrop addresses have an outdated format and need to be transformed to find your accounts on block explorers like Subscan.io. Subscan has a great tool for this, you can enter your public address to see the full list of network transformations of your address. You'll want to copy the one for Edgeware. Scroll down for background or more ways to do this.

[https://edgeware.subscan.io/tools/ss58\_transform](https://edgeware.subscan.io/tools/ss58\_transform)

![](<../../.gitbook/assets/screen-shot-2020-07-22-at-5.47.26-pm (2) (1) (1) (1).png>)

### Background

During the lockdrop, the keypairs that were generated with Subkey were encoded using the Subkey Default Network ID. This impacts the Public Address (SS58 Address Format) that Subkey outputs in certain cases. The secret phrase/seed, and public key are not impacted by this change.

1. You can always use the Default-Network-ID-encoded Public Address to **receive** funds safely.
2. However, It is a 'best practice' to use the \_new Edgeware-\_network-ID version of your address when interacting with the Edgeware network, including sending funds.
3. You will need to re-generate your public address to use some Block Explorer tools. At this time, Polkascan uses the new Edgeware network ID encoding.

You can also get the new version of your address in two other ways - the Polkadot UI or the Subkey tool.

{% hint style="warning" %}
The Polkadot.js **Browser Extension** does not display the Edgeware network ID encoded at this time, **but the Polkadot UI does.**
{% endhint %}

{% tabs %}
{% tab title="Easy Mode: Subscan Tool" %}
[Visit this Subscan Tool](https://edgeware.subscan.io/tools/ss58\_transform) and enter your address or public key to generate a list of many network-encoded versions of your address. Save the one marked Edgeware.

![](<../../.gitbook/assets/image (14) (4) (4) (4) (4).png>)
{% endtab %}

{% tab title="Using Polkadot UI" %}
The easiest way to get your Edgeware network ID version of your public address is to use the Account or Address Book tool of [the Polkadot UI.](https://polkadot.js.org/apps/#/explorer)

Enter your old address into the search bar in the Address Book tool, and then click the identicon to the left as shown in the image below. It will copy your current Edgeware network encoded address. Store this safely.

Alternatively, you can use the Accounts tab to do the same if you've connected via the Polkadot UI Browser Extension.

![](<../../.gitbook/assets/screen-shot-2020-03-06-at-3.25.07-pm (2) (2) (2) (2).png>)
{% endtab %}

{% tab title="Using Subkey CLI" %}
{% hint style="info" %}
This process requires the latest version of the Subkey program in order to select Edgeware as the network.
{% endhint %}

You can generate a new key with the Edgeware network ID using

```
subkey -n edgeware generate
```

You can also derive the SS58 Address from **an existing key OR address** with the Edgeware Network ID by using

```
subkey -n edgeware inspect "INSERT MNEMONIC/EXISTING ADDRESS HERE"
```

### Examples

In order of examples:

1. Generate a new key with `subkey -n edgeware`
2. Inspect key with default network ID (as you can see the SS58 is different)
3. Inspect key with **edgeware network ID** (as you can see it matches the first example entirely)

```
➜ subkey -n edgeware generate

Secret phrase `submit hotel naive plate among decorate ghost speak exchange mimic sentence bar` is account:
  Secret seed:      0xbe59988b1ad6e93325766b9ca8713db866538f75b578f714cffa3583f9978a23
  Public key (hex): 0x0045d45397c474d6a4fddb00e314637c8970be097f5a9a2b950dc2ea74a00849
  Account ID:       0x0045d45397c474d6a4fddb00e314637c8970be097f5a9a2b950dc2ea74a00849
  SS58 Address:     hWyZ5UkvkrPpmiD3MJ7htdhEigxFe34pUH3Dy9Pq71QeZg4

  ➜ subkey inspect "submit hotel naive plate among decorate ghost speak exchange mimic sentence bar"

Secret phrase `submit hotel naive plate among decorate ghost speak exchange mimic sentence bar` is account:
  Secret seed:      0xbe59988b1ad6e93325766b9ca8713db866538f75b578f714cffa3583f9978a23
  Public key (hex): 0x0045d45397c474d6a4fddb00e314637c8970be097f5a9a2b950dc2ea74a00849
  Account ID:       0x0045d45397c474d6a4fddb00e314637c8970be097f5a9a2b950dc2ea74a00849
  SS58 Address:     5C54boRsNwTqHpsSjz5wvRwZrhhFB45HRPfdktew32pUW8CZ

  ➜ subkey -n edgeware inspect "submit hotel naive plate among decorate ghost speak exchange mimic sentence bar"

Secret phrase `submit hotel naive plate among decorate ghost speak exchange mimic sentence bar` is account:
  Secret seed:      0xbe59988b1ad6e93325766b9ca8713db866538f75b578f714cffa3583f9978a23
  Public key (hex): 0x0045d45397c474d6a4fddb00e314637c8970be097f5a9a2b950dc2ea74a00849
  Account ID:       0x0045d45397c474d6a4fddb00e314637c8970be097f5a9a2b950dc2ea74a00849
  SS58 Address:     hWyZ5UkvkrPpmiD3MJ7htdhEigxFe34pUH3Dy9Pq71QeZg4
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
On Commonwealth.im, when Edgeware mainnet is enabled, the inputs will auto-derive the SS58 with the correct network ID, however, using the default-ID-ss58 outside of Commonwealth.im will likely result in errors that may endanger funds. To be safe, always use the Edgeware Network ID SS58 Address.
{% endhint %}

## Connect Your Account

There are several ways to connect your existing account from the Lockdrop or other events to an account manager or wallet.

First, install the [Polkadot.js Browser Extension](https://github.com/polkadot-js/extension):

{% tabs %}
{% tab title="Polkadot.js Extension" %}
* On Chrome, install via [Chrome web store](https://chrome.google.com/webstore/detail/polkadot%7Bjs%7D-extension/mopnmbcafieddcagagdcbnhejhlodfdd)
* On Firefox, install via [Firefox add-ons](https://addons.mozilla.org/en-US/firefox/addon/polkadot-js-extension/)
* You will need your seed phrase, a series of words.

Next, click the Orange P icon in your browser extension section.

Click the button stating "I have a pre-existing seed, import the account."

Enter your mnemonic phrase and hit the confirm button.

Next, visit [https://polkadot.js.org/apps/#/explorer](https://polkadot.js.org/apps/#/explorer), ensure you are connected to [the Edgeware network](https://github.com/hicommonwealth/edgeware-documentation/blob/master/docs/other-resources/networks.md) by clicking the top left network logo and selecting the network you want to connect to.

Once connected, the extension will prompt you to authorize connecting your local wallet to the service.Select your account, enter your wallet password and authorize the interaction.

You can now explore the chain and your account on Edgeware.

![](<../../.gitbook/assets/screen-shot-2020-02-10-at-3.03.43-am (2) (2) (2) (2).png>)
{% endtab %}

{% tab title="Commonwealth.im" %}
Finally, enter in a name and password twice for your newly connected account. Once connected, you can visit [https://polkadot.js.org/apps/#/explorer](https://polkadot.js.org/apps/#/explorer), connect to the Edgeware testnet, and view your balance and interact with the chain.
{% endtab %}
{% endtabs %}

## Check your Balance via Block Explorer

At this time, the two main block explorers are

* [Polkascan](https://polkascan.io/pre/edgeware-berlin)
* [Subscan](https://edgeware.subscan.io)

Both of these explorers will only work with Public Addresses (SS58) that have the Edgeware network ID encoded.

{% hint style="info" %}
If you have not re-encoded your public address from you Lockdrop-created keypair with the new Edgeware network ID, you **must do so** in order to use block explorers to find your account. Follow the instructions linked below.
{% endhint %}

Once you have your re-encoded Public Address, you can enter it into the search bar in a block explorer to pull up your account and view the balance.
