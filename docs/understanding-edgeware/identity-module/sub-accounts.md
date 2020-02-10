# Sub Accounts

Users can also link accounts by setting "sub accounts", each with its own identity, under a primary account. The system reserves a bond of 2 EDG for each sub account. An example of how you might use this would be a validation company running multiple validators. A single entity, "My Staking Company", could register multiple sub accounts that represent the [Stash accounts](https://wiki.polkadot.network/docs/en/learn-keys) of each of their validators.

{% hint style="info" %}
**Parameter Note:** The Sub Account Bond, the returnable fee charged for adding a sub-account, is 2 EDG per sub-account.
{% endhint %}

{% hint style="info" %}
**Parameter Note:** The Sub-account limit, the amount of sub-accounts an account may have, is 100.
{% endhint %}

To register a sub-account on an existing account, you must currently use the [Extrinsics UI](https://polkadot.js.org/apps/#/extrinsics). There, select the identity pallet, then `setSubs` as the function to use. Click "Add Item" for every child account you want to add to the parent sender account. The value to put into the Data field of each parent is the optional name of the sub-account. If omitted, the sub-account will inherit the parent's name and be displayed as `parent/parent` instead of `parent/child`.

![Sub account setup](https://wiki.polkadot.network/img/identity/06.jpg)

Note that a deposit is required for every sub-account.

