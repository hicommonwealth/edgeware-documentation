# Making Transaction with a multi-signature account

There are three types of actions you can take with a multi-sig account:

* Executing a call.
* Approving a call.
* Cancelling a call.

In scenarios where only a single approval is needed, a convenience method `as_multi_threshold_1` should be used. This function takes only the other signatories and the raw call as its arguments.

However, in any case besides a single approval, you will likely need more than one of the signatories to approve the call before finally executing it. When you create a new call or approve a call as a multi-sig, you will need to place a small deposit. The deposit stays locked in the pallet until the call is executed. The reason for the deposit is to place an economic cost on the storage space that the multi-sig call takes up on the chain and discourage users from creating dangling multi-sig operations that never get executed. The deposit will be reserved in the caller's accounts so participants in multi-signature wallets should have spare funds available.

The deposit is dependent on the threshold parameter and is calculated as follows:

```text
Deposit = DepositBase + threshold * DepositFactor
```

Where `DepositBase` and `DepositFactor` are chain constants set in the runtime code.

Currently, the DepositBase is equal to `deposit(1, 88)` and the DepositFactor is equal to `deposit(0,32)`.

