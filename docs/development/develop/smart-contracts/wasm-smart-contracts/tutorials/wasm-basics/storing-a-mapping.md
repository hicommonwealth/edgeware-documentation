# Incrementing My Value

The final step in our Incrementer contract is to allow each user to update increment their own value.

## Modifying a HashMap <a id="modifying-a-hashmap"></a>

Making changes to the value of a HashMap is just as sensitive as getting the value. If you try to modify some value before it has been initialized, your contract will panic!

But have no fear, we can continue to use the `my_number_or_zero` function we created to protect us from these situations!

```rust
impl MyContract {

    /* --snip-- */

    // Set the value for the calling AccountId
    #[ink(message)]
    pub fn set_my_number(&mut self, value: u32) {
        let caller = self.env().caller();
        self.my_number_map.insert(caller, value);
    }

    // Add a value to the existing value for the calling AccountId
    #[ink(message)]
    pub fn add_my_number(&mut self, value: u32) {
        let caller = self.env().caller();
        let my_number = self.my_number_or_zero(&caller);
        self.my_number_map.insert(caller, my_number + value);
    }

    /// Returns the number for an AccountId or 0 if it is not set.
    fn my_number_or_zero(&self, of: &AccountId) -> u32 {
        *self.my_number_map.get(of).unwrap_or(&0)
    }
}
```

Here we have written two kinds of functions which modify a HashMap. One which simply inserts the value directly into storage, with no need to read the value first, and the other which modifies the existing value. Note how we can always `insert` the value without worry, as that initialized the value in storage, but before you can get or modify anything, we need to call `my_number_or_zero` to make sure we are working with a real value.

## Feel the Pain \(Optional\) <a id="feel-the-pain-optional"></a>

We will not always have an existing value on our contract's storage. We can take advantage of the Rust `Option<T>` type to help use on this task. If there's no value on the contract storage we will insert a new one; on the contrary if there is an existing value we will only update it.

ink! HashMaps expose the well-known `entry` API that we can use to achieve this type of "upset" behavior:

```rust
let caller = self.env().caller();
self.my_number_map
    .entry(caller)
    .and_modify(|old_value| old_value += by)
    .or_insert(by);
```

## Your Turn! <a id="your-turn"></a>

Follow the `ACTION`s to finish your Incrementer smart contract.

Remember to run `cargo +nightly test` to test your work.

{% tabs %}
{% tab title="🔨Starting Point" %}
```rust
#![cfg_attr(not(feature = "std"), no_std)]

use ink_lang as ink;

#[ink::contract]
mod incrementer {
    #[ink(storage)]
    pub struct Incrementer {
        value: i32,
        my_value: ink_storage::collections::HashMap<AccountId, u64>,
    }

    impl Incrementer {
        #[ink(constructor)]
        pub fn new(init_value: i32) -> Self {
            Self {
                value: init_value,
                my_value: ink_storage::collections::HashMap::new(),
            }
        }

        #[ink(constructor)]
        pub fn default() -> Self {
            Self {
                value: 0,
                my_value: Default::default(),
            }
        }

        #[ink(message)]
        pub fn get(&self) -> i32 {
            self.value
        }

        #[ink(message)]
        pub fn inc(&mut self, by: i32) {
            self.value += by;
        }

        #[ink(message)]
        pub fn get_mine(&self) -> u64 {
            self.my_value_or_zero(&self.env().caller())
        }

        #[ink(message)]
        pub fn inc_mine(&mut self, by: u64) {
            // ACTION: Get the `caller` of this function.
            // ACTION: Get `my_value` that belongs to `caller` by using `my_value_or_zero`.
            // ACTION: Insert the incremented `value` back into the mapping.
        }

        fn my_value_or_zero(&self, of: &AccountId) -> u64 {
            *self.my_value.get(of).unwrap_or(&0)
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
mod incrementer {
    #[ink(storage)]
    pub struct Incrementer {
        value: i32,
        my_value: ink_storage::collections::HashMap<AccountId, u64>,
    }

    impl Incrementer {
        #[ink(constructor)]
        pub fn new(init_value: i32) -> Self {
            Self {
                value: init_value,
                my_value: ink_storage::collections::HashMap::new(),
            }
        }

        #[ink(constructor)]
        pub fn default() -> Self {
            Self {
                value: 0,
                my_value: Default::default(),
            }
        }

        #[ink(message)]
        pub fn get(&self) -> i32 {
            self.value
        }

        #[ink(message)]
        pub fn inc(&mut self, by: i32) {
            self.value += by;
        }

        #[ink(message)]
        pub fn get_mine(&self) -> u64 {
            self.my_value_or_zero(&self.env().caller())
        }

        #[ink(message)]
        pub fn inc_mine(&mut self, by: u64) {
            let caller = self.env().caller();
            let my_value = self.my_value_or_zero(&caller);
            self.my_value.insert(caller, my_value + by);
        }

        fn my_value_or_zero(&self, of: &AccountId) -> u64 {
            *self.my_value.get(of).unwrap_or(&0)
        }
    }

    #[cfg(test)]
    mod tests {
        use super::*;
```
{% endtab %}
{% endtabs %}

