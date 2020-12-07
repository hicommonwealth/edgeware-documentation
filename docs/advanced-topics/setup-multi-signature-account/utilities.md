# Utilities

## Generating Addresses of Multi-signature Accounts

> NOTE: Addresses that are provided to the multi-sig wallets must be sorted. The below methods for generating sort the accounts for you, but if you are implementing your own sorting then be aware that the public keys are compared byte-for-byte and sorted ascending before being inserted in the payload that is hashed.

Addresses are deterministically generated from the signers and threshold of the multisig wallet. The [w3f/msig-util](https://www.npmjs.com/package/@w3f/msig-util) is a small CLI tool that can determine the multisignature address based on your inputs.

You can see here, we took addresses of development accounts ALICE, BOB and CHARLIE and we've got same address, that we have in our Apps.

```text
❯ npx @w3f/msig-util derive --addresses 5GrwvaEF5zXb26Fz9rcQpDWS57CtERHpNehXCPcNoHGKutQY,5FHneW46xGXgs5mUiveU4sbTyGBzmstUspZC92UhjJM694ty,5FLSigC9HGRKVhB9FiEo4Y3koPsNmBmLJbpXg2mp1hXcS59Y --threshold 2 --ss58Prefix 42
--------------------------------
Addresses: 5GrwvaEF5zXb26Fz9rcQpDWS57CtERHpNehXCPcNoHGKutQY 5FHneW46xGXgs5mUiveU4sbTyGBzmstUspZC92UhjJM694ty 5FLSigC9HGRKVhB9FiEo4Y3koPsNmBmLJbpXg2mp1hXcS59Y
Threshold: 2
Multisig Address (SS58: 42): 5DjYJStmdZ2rcqXbXGX7TW85JsrW6uG4y9MUcLq2BoPMpRA7
--------------------------------
```

* [w3f/msig-util](https://www.npmjs.com/package/@w3f/msig-util) - [internal code](https://github.com/lsaether/msig-util/blob/master/src/actions/deriveAddress.ts)

