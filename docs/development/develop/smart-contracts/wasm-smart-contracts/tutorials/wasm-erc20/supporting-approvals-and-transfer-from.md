# Supporting Approvals and Transfer From

We are almost there! Our token contract can now transfer funds from user to user and tell the outside world what is going on when this happens. All that is left to do is introduce the `approve` and `transfer_from` functions.

## Third Party Transfers <a id="third-parity-transfers"></a>

This section is all about adding the ability for other accounts to safely spend some amount of your tokens.

The immediate question should be: "Why the heck would I want that?"

Well, one such scenario is to support Decentralized Exchanges. Basically, other smart contracts can allow you to exchange tokens with other users, usually one type of token for another. However, these "bids" do not always execute right away. Maybe you want to get a really good deal for token trade, and will hold out until that trade is met.

Well, rather than giving your tokens directly to the contract \(an escrow\), you can simply "approve" them to spend some of your tokens on your behalf! This means that during the time while you are waiting for a trade to execute, you can still control and spend your funds if needed. Better yet, you can approve multiple different contracts or users to access your funds, so if one contract offers the best trade, you do not need to pull out funds from the other and move them, a sometimes costly and time consuming process.

So hopefully you can see why a feature like this would be useful, but how can we do it safely?

We use a two step process: **Approve** and **Transfer From**.

### Approve <a id="approve"></a>

Approving another account to spend your funds is the first step in the third party transfer process. A token owner can specify another account and any arbitrary number of tokens it can spend on the owner's behalf. The owner need not have all their funds approved to be spent by others; in the situation where there is not enough funds, the approved account can spend up to the approved amount from the owner's balance.

When an account calls `approve` multiple times, the approved value simply overwrites any existing value that was approved in the past. By default, the approved value between any two accounts is `0`, and a user can always call approve for `0` to revoke access to their funds from another account.

To store approvals in our contract, we need to use a slightly fancy `HashMap`.

Since each account can have a different amount approved for any other account to use, we need to use a tuple as our key which simply points to a balance value. Here is an example of what that would look like:

```rust
pub struct Erc20 {
    /// Balances that are spendable by non-owners: (owner, spender) -> allowed
    allowances: ink_storage::collections::HashMap<(AccountId, AccountId), Balance>,
}
```

Here we have defined the tuple to represent `(owner, spender)` such that we can look up how much a "spender" can spend from an "owner's" balance using the `AccountId`s in this tuple. Remember that we will need to again create an `allowance_of_or_zero` function to help us get the allowance of an account when it is not initialized, and a getter function called `allowance` to look up the current value for any pair of accounts.

```rust
/// Approve the passed AccountId to spend the specified amount of tokens
/// on the behalf of the message's sender.
#[ink(message)] 
pub fn approve(&mut self, spender: AccountId, value: Balance) -> bool {/* --snip-- */}
```

When you call the `approve` function, you simply insert the `value` specified into storage. The `owner` is always the `self.env().caller()`, ensuring that the function call is always authorized.

### Transfer From <a id="transfer-from"></a>

Finally, once we have set up an approval for one account to spend on-behalf-of another, we need to create a special `transfer_from` function which enables an approved user to transfer those funds.

As mentioned earlier, we will take advantage of the private `transfer_from_to` function to do the bulk of our transfer logic. All we need to introduce is the _authorization_ logic again.

So what does it mean to be authorized to call this function?

1. The `self.env().caller()` must have some allowance to spend funds from the `from` account.
2. The allowance must not be less than the value trying to be transferred.

In code, that can easily be represented like so:

```rust
let allowance = self.allowance_of_or_zero(&from, &self.env().caller());
if allowance < value {
    return false
}
/* --snip-- */
true
```

Again, we exit early and return false if our authorization does not pass.

If everything looks good though, we simply `insert` the updated allowance into the `allowance` HashMap \(`let new_allowance = allowance - value`\), and call the `transfer_from_to` between the specified `from` and `to` accounts.

## Be Careful! <a id="be-careful"></a>

If you glaze over the logic of this function too quickly, you may introduce a bug into your smart contract. Remember when calling `transfer_from`, the `self.env().caller()` and the `from` account is used to look up the current allowance, but the `transfer_from` function is called between the `from` and `to` account specified.

There are three account variables in play whenever `transfer_from` is called, and you need to make sure to use them correctly! Hopefully our test will catch any mistake you make.

## Your Turn! <a id="your-turn"></a>

You are almost there! This is the last piece of the ERC20 token contract.

Follow the `ACTION`s in the contract template to finish your ERC20 implementation.

Remember to run `cargo +nightly test` to test your work.

{% tabs %}
{% tab title="🔨Starting Point" %}
```rust
#![cfg_attr(not(feature = "std"), no_std)]

use ink_lang as ink;

#[ink::contract]
mod erc20 {
    #[cfg(not(feature = "ink-as-dependency"))]
    #[ink(storage)]
    pub struct Erc20 {
        /// The total supply.
        total_supply: Balance,
        /// The balance of each user.
        balances: ink_storage::collections::HashMap<AccountId, Balance>,
        /// Approval spender on behalf of the message's sender.
        allowances: ink_storage::collections::HashMap<(AccountId, AccountId), Balance>,
    }

    #[ink(event)]
    pub struct Transfer {
        #[ink(topic)]
        from: Option<AccountId>,
        #[ink(topic)]
        to: Option<AccountId>,
        #[ink(topic)]
        value: Balance,
    }

    #[ink(event)]
    pub struct Approval {
        #[ink(topic)]
        owner: AccountId,
        #[ink(topic)]
        spender: AccountId,
        #[ink(topic)]
        value: Balance,
    }

    impl Erc20 {
        #[ink(constructor)]
        pub fn new(initial_supply: Balance) -> Self {
            let caller = Self::env().caller();
            let mut balances = ink_storage::collections::HashMap::new();
            balances.insert(caller, initial_supply);

            Self::env().emit_event(Transfer {
                from: None,
                to: Some(caller),
                value: initial_supply,
            });

            Self {
                total_supply: initial_supply,
                balances,
                allowances: ink_storage::collections::HashMap::new(),
            }
        }

        #[ink(message)]
        pub fn total_supply(&self) -> Balance {
            self.total_supply
        }

        #[ink(message)]
        pub fn balance_of(&self, owner: AccountId) -> Balance {
            self.balance_of_or_zero(&owner)
        }

        #[ink(message)]
        pub fn approve(&mut self, spender: AccountId, value: Balance) -> bool {
            // Record the new allowance.
            let owner = self.env().caller();
            self.allowances.insert((owner, spender), value);

            // Notify offchain users of the approval and report success.
            self.env().emit_event(Approval {
                owner,
                spender,
                value,
            });
            true
        }

        #[ink(message)]
        pub fn allowance(&self, owner: AccountId, spender: AccountId) -> Balance {
            self.allowance_of_or_zero(&owner, &spender)
        }

        #[ink(message)]
        pub fn transfer_from(&mut self, from: AccountId, to: AccountId, value: Balance) -> bool {
            // Ensure that a sufficient allowance exists.
            let caller = self.env().caller();
            let allowance = self.allowance_of_or_zero(&from, &caller);
            if allowance < value {
                return false;
            }

            // Decrease the value of the allowance and transfer the tokens.
            self.allowances.insert((from, caller), allowance - value);
            self.transfer_from_to(from, to, value)
        }

        #[ink(message)]
        pub fn transfer(&mut self, to: AccountId, value: Balance) -> bool {
            self.transfer_from_to(self.env().caller(), to, value)
        }

        fn transfer_from_to(&mut self, from: AccountId, to: AccountId, value: Balance) -> bool {
            let from_balance = self.balance_of_or_zero(&from);
            if from_balance < value {
                return false
            }

            // Update the sender's balance.
            self.balances.insert(from, from_balance - value);

            // Update the receiver's balance.
```
{% endtab %}

{% tab title="✅Potential Solution" %}
```rust
#![cfg_attr(not(feature = "std"), no_std)]

use ink_lang as ink;

#[ink::contract(version = "0.1.0")]
mod erc20 {
    use ink_core::storage;

    #[ink(storage)]
    struct Erc20 {
        /// The total supply.
        total_supply: storage::Value<Balance>,
        /// The balance of each user.
        balances: storage::HashMap<AccountId, Balance>,
        /// Approval spender on behalf of the message's sender.
        allowances: storage::HashMap<(AccountId, AccountId), Balance>,
    }

    #[ink(event)]
    struct Transfer {
        #[ink(topic)]
        from: Option<AccountId>,
        #[ink(topic)]
        to: Option<AccountId>,
        #[ink(topic)]
        value: Balance,
    }

    #[ink(event)]
    struct Approval {
        #[ink(topic)]
        owner: AccountId,
        #[ink(topic)]
        spender: AccountId,
        #[ink(topic)]
        value: Balance,
    }

    impl Erc20 {
        #[ink(constructor)]
        fn new(&mut self, initial_supply: Balance) {
            let caller = self.env().caller();
            self.total_supply.set(initial_supply);
            self.balances.insert(caller, initial_supply);
            self.env().emit_event(Transfer {
                from: None,
                to: Some(caller),
                value: initial_supply,
            });
        }

        #[ink(message)]
        fn total_supply(&self) -> Balance {
            *self.total_supply
        }

        #[ink(message)]
        fn balance_of(&self, owner: AccountId) -> Balance {
            self.balance_of_or_zero(&owner)
        }

        #[ink(message)]
        fn approve(&mut self, spender: AccountId, value: Balance) -> bool {
            let owner = self.env().caller();
            self.allowances.insert((owner, spender), value);
            self.env().emit_event(Approval {
                owner,
                spender,
                value,
            });
            true
        }

        #[ink(message)]
        fn allowance(&self, owner: AccountId, spender: AccountId) -> Balance {
            self.allowance_of_or_zero(&owner, &spender)
        }

        #[ink(message)]
        fn transfer_from(&mut self, from: AccountId, to: AccountId, value: Balance) -> bool {
            let caller = self.env().caller();
            let allowance = self.allowance_of_or_zero(&from, &caller);
            if allowance < value {
                return false
            }
            self.allowances.insert((from, caller), allowance - value);
            self.transfer_from_to(from, to, value)
        }

        #[ink(message)]
        fn transfer(&mut self, to: AccountId, value: Balance) -> bool {
            let from = self.env().caller();
            self.transfer_from_to(from, to, value)
        }

        fn transfer_from_to(&mut self, from: AccountId, to: AccountId, value: Balance) -> bool {
            let from_balance = self.balance_of_or_zero(&from);
            if from_balance < value {
                return false
            }
            let to_balance = self.balance_of_or_zero(&to);
            self.balances.insert(from, from_balance - value);
            self.balances.insert(to, to_balance + value);
            self.env().emit_event(Transfer {
                from: Some(from),
                to: Some(to),
                value,
            });
            true
        }

        fn balance_of_or_zero(&self, owner: &AccountId) -> Balance {
            *self.balances.get(owner).unwrap_or(&0)
        }
```
{% endtab %}
{% endtabs %}

