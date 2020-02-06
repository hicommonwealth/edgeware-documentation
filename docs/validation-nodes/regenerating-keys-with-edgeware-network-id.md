# Regenerating Keys with Edgeware Network ID



You can generate a new key with the Edgeware network ID using

```text
subkey -n edgeware generate
```

You can also derive the SS58 Address from **an existing key** with the Edgeware Network ID by using

```text
subkey -n edgeware inspect "INSERT MNEMONIC HERE" 
```

{% hint style="info" %}
On Commonwealth.im, when Edgeware mainnet is enabled, the inputs will auto-derive the SS58 with the correct network ID, however, using the default-ID-ss58 outside of Commonwealth.im will likely result in serious errors that may endanger funds. To be safe, always use the Edgeware Network ID SS58 Address.
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

