# Regenerating Public Addresses with the Edgeware Network ID

## Background

During the lockdrop, the keypairs that were generated with Subkey were encoded using the Subkey Default Network ID.  This impacts the Public Address \(SS58 Address Format\) that Subkey outputs in certain cases. The secret phrase/seed, and public key are not impacted by this change.

1. You can always use the Default-Network-ID-encoded Public Address to **receive** funds safely.
2.  However, It is a 'best practice' to use the _new Edgeware-_network-ID version of your address when interacting with the Edgeware network, including sending funds.
3. You will need to re-generate your public address to use some Block Explorer tools. At this time, Polkascan uses the new Edgeware network ID encoding. 

You can get the new version of your address in two ways - the Polkadot UI or the Subkey tool. 

{% hint style="warning" %}
The Polkadot.js **Browser Extension** does not display the Edgeware network ID encoded at this time, **but the Polkadot UI does.**
{% endhint %}

## Steps

{% tabs %}
{% tab title="Using Polkadot UI" %}
The easiest way to get your Edgeware network ID version of your public address is to use the Account or Address Book tool of [the Polkadot UI. ](https://polkadot.js.org/apps/#/explorer)

Enter your old address into the search bar in the Address Book tool, and then click the identicon to the left as shown in the image below. It will copy your current Edgeware network encoded address. Store this safely. 

Alternatively, you can use the Accounts tab to do the same if you've connected via the Polkadot UI Browser Extension.

![](../../.gitbook/assets/screen-shot-2020-03-06-at-3.25.07-pm.png)
{% endtab %}

{% tab title="Using Subkey CLI" %}
{% hint style="info" %}
This process requires the latest version of the Subkey program in order to select Edgeware as the network. 
{% endhint %}

You can generate a new key with the Edgeware network ID using

```text
subkey -n edgeware generate
```

You can also derive the SS58 Address from **an existing key OR address** with the Edgeware Network ID by using

```text
subkey -n edgeware inspect "INSERT MNEMONIC/EXISTING ADDRESS HERE" 
```

## Examples

  
In order of examples:

1. Generate a new key with `subkey -n edgeware`
2. Inspect key with default network ID \(as you can see the SS58 is different\)
3. Inspect key with **edgeware network ID** \(as you can see it matches the first example entirely\)

```text
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

