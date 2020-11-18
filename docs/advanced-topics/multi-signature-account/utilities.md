## Utilities 

### Generating Addresses of Multi-signature Accounts

> NOTE: Addresses that are provided to the multi-sig wallets must be sorted. The below methods for generating sort the accounts for you, but if you are implementing your own sorting then be aware that the public keys are compared byte-for-byte and sorted ascending before being inserted in the payload that is hashed.

Addresses are deterministically generated from the signers and threshold of the multisig wallet. 
The [w3f/msig-util](https://www.npmjs.com/package/@w3f/msig-util) is a small CLI tool that can determine the multisignature address based on your inputs. 

* [w3f/msig-util](https://www.npmjs.com/package/@w3f/msig-util) - [internal code](https://github.com/lsaether/msig-util/blob/master/src/actions/deriveAddress.ts)