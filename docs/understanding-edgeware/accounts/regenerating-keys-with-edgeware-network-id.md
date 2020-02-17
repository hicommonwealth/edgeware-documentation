# Regenerating Public Addresses with the Edgeware Network ID

## Background

During the lockdrop, the keypairs that were generated with Subkey were encoded using the Subkey Default Network ID.  This impacts the Public Address \(SS58 Address Format\) that Subkey outputs in certain cases. The secret phrase/seed, and public key are not impacted by this change.

1. You can always use the Default-Network-ID-encoded Public Address to **receive** funds safely.
2.  However, It is a 'best practice' to use the new Edgeware-network-ID version of your address when interacting with the Edgeware network, including sending funds.
3. You will need to re-generate your public address to use some Block Explorer tools. At this time, Polkascan utilizes the new Edgeware network ID encoding. 

{% hint style="info" %}
The Polkadot.js Browser Extension does not display the Edgeware network ID encoded at this time. The public address of your EDG wallet shown in the extension is encoded using the 'default network ID' of Subkey, the program that generates keypairs for Substrate-based chains. As a result, the public addresses shown may not be useful for using block explorers. 
{% endhint %}

## Steps

{% hint style="info" %}
This process requires the latest version of the Subkey program in order to select Edgeware as the network. 
{% endhint %}

You can generate a new key with the Edgeware network ID using

```text
subkey -n edgeware generate
```

You can also derive the SS58 Address from **an existing key** with the Edgeware Network ID by using

```text
subkey -n edgeware inspect "INSERT MNEMONIC HERE" 
```

{% hint style="info" %}
On Commonwealth.im, when Edgeware mainnet is enabled, the inputs will auto-derive the SS58 with the correct network ID, however, using the default-ID-ss58 outside of Commonwealth.im will likely result in errors that may endanger funds. To be safe, always use the Edgeware Network ID SS58 Address.
{% endhint %}

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

