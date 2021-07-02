# Transferring Tokens

So at this point, we have a single user that owns all the tokens for the contract. However, it's not _really_ a useful token unless you can transfer them to other people...

Let's do that!

## The Transfer Function <a id="the-transfer-function"></a>

The `transfer` function does exactly what you might expect: it allows the user calling the contract to transfer some funds they own to another user.

You will notice in our template code there is a public function `transfer` and an internal function `transfer_from_to`. We have done this because in the future, we will be reusing the logic for a token transfer when we enable third party allowances and spending on-behalf-of.

### transfer\_from\_to\(\) <a id="transfer_from_to"></a>

```rust
fn transfer_from_to(&mut self, from: AccountId, to: AccountId, value: Balance) -> bool {/* --snip-- */}
```

The `transfer_from_to` function will be built without any _authorization_ checks. Because it is an internal function, we fully control when it gets called. However, it will have all logical checks around managing the balances between accounts.

Really we just need to check for one thing: make sure that the `from` account has enough funds to send to the `to` account:

```rust
if balance_from < value {
    return false
}
```

Remember that the `transfer` function and other public functions return a bool to indicate success. If the `from` account does not have enough balance to satisfy the transfer, we will exit early and return false, not making any changes to the contract state. Our `transfer_from_to` will simply forward the "success" `bool` up to the function that calls it.

### transfer\(\) <a id="transfer"></a>

```rust
#[ink(message)] 
pub fn transfer(&mut self, to: AccountId, value: Balance) -> bool {/* --snip-- */}
```

Finally, the `transfer` function will simply call into the `transfer_from_to` with the `from` parameter automatically set to the `self.env().caller()`. This is our "authorization check" since the contract caller is always authorized to move their own funds.

## Transfer Math <a id="transfer-math"></a>

There really is not much to say about the simple math executed within a token transfer.

1. First we get the current balance of both the `from` and `to` account, making sure to use our `balance_of_or_zero()` getter.
2. Then we make the logic check mentioned above to ensure the `from` balance has enough funds to send `value`.
3. Finally, we subtract that `value` from the `from` balance and add it to the `to` balance and insert those new values back in.

## Your Turn! <a id="your-turn"></a>

Follow the `ACTION`s in the template code to build your transfer function.

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
    }

    impl Erc20 {
        #[ink(constructor)]
        pub fn new(initial_supply: Balance) -> Self {
            let mut balances = ink_storage::collections::HashMap::new();
            balances.insert(Self::env().caller(), initial_supply);
            Self {
                total_supply: initial_supply,
                balances
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
        pub fn transfer(&mut self, to: AccountId, value: Balance) -> bool {
            // ACTION: Call the `transfer_from_to` with `from` as `self.env().caller()`
        }

        fn transfer_from_to(&mut self, from: AccountId, to: AccountId, value: Balance) -> bool {
            // ACTION: Get the balance for `from` and `to`
            //   HINT: Use the `balance_of_or_zero` function to do this
            // ACTION: If `from_balance` is less than `value`, return `false`
            // ACTION: Insert new values for `from` and `to`
            //         * from_balance - value
            //         * to_balance + value
            // ACTION: Return `true`
        }

        fn balance_of_or_zero(&self, owner: &AccountId) -> Balance {
            *self.balances.get(owner).unwrap_or(&0)
        }
    }

    #[cfg(test)]
    mod tests {
        use super::*;
```
{% endtab %}

{% tab title="✅Potential Solution" %}
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
    }

    impl Erc20 {
        #[ink(constructor)]
        pub fn new(initial_supply: Balance) -> Self {
            let mut balances = ink_storage::collections::HashMap::new();
            balances.insert(Self::env().caller(), initial_supply);
            Self {
                total_supply: initial_supply,
                balances
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
            let to_balance = self.balance_of_or_zero(&to);
            self.balances.insert(to, to_balance + value);

            true
        }

        fn balance_of_or_zero(&self, owner: &AccountId) -> Balance {
            *self.balances.get(owner).unwrap_or(&0)
        }
```
{% endtab %}
{% endtabs %}

