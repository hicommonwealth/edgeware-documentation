# Storing a Mapping

## Storing a Mapping <a id="storing-a-mapping"></a>

Let's now extend our Incrementer to not only manage one number, but to manage one number per user!

### Storage HashMap <a id="storage-hashmap"></a>

In addition to storing individual values, ink! also supports a `HashMap` which allows you to store items in a key-value mapping.

Here is an example of a mapping from user to a number:

```rust
#[ink(storage)]
pub struct MyContract {
    // Store a mapping from AccountIds to a u32
    my_number_map: ink_storage::collections::HashMap<AccountId, u32>,
}
```

This means that for a given key, you can store a unique instance of a value type. In this case, each "user" gets their own number, and we can build logic so that only they can modify their own number.

### Storage HashMap API <a id="storage-hashmap-api"></a>

You can find the full HashMap API in the [crates/storage/src/collections/hashmap](https://github.com/paritytech/ink/blob/master/crates/storage/src/collections/hashmap/mod.rs) part of ink!.

Here are some of the most common functions you might use:

```rust
    /// Inserts a key-value pair into the map.
    ///
    /// Returns the previous value associated with the same key if any.
    /// If the map did not have this key present, `None` is returned.
    pub fn insert(&mut self, key: K, new_value: V) -> Option<V> {/* --snip-- */}

    /// Removes the key/value pair from the map associated with the given key.
    ///
    /// - Returns the removed value if any.
    pub fn take<Q>(&mut self, key: &Q) -> Option<V> {/* --snip-- */}

    /// Returns a shared reference to the value corresponding to the key.
    ///
    /// The key may be any borrowed form of the map's key type,
    /// but `Hash` and `Eq` on the borrowed form must match those for the key type.
    pub fn get<Q>(&self, key: &Q) -> Option<&V> {/* --snip-- */}

    /// Returns a mutable reference to the value corresponding to the key.
    ///
    /// The key may be any borrowed form of the map's key type,
    /// but `Hash` and `Eq` on the borrowed form must match those for the key type.
    pub fn get_mut<Q>(&mut self, key: &Q) -> Option<&mut V> {/* --snip-- */}

    /// Returns `true` if there is an entry corresponding to the key in the map.
    pub fn contains_key<Q>(&self, key: &Q) -> bool {/* --snip-- */}

    /// Converts the OccupiedEntry into a mutable reference to the value in the entry
    /// with a lifetime bound to the map itself.
    pub fn into_mut(self) -> &'a mut V {/* --snip-- */}

    /// Gets the given key's corresponding entry in the map for in-place manipulation.
    pub fn entry(&mut self, key: K) -> Entry<K, V> {/* --snip-- */}Copy to clipboardErrorCopied
```

### Initializing a HashMap <a id="initializing-a-hashmap"></a>

As mentioned, not initializing storage before you use it is a common error that can break your smart contract. For each key in a storage value, the value needs to be set before you can use it. To do this, we will create a private function which handles when the value is set and when it is not, and make sure we never work with uninitialized storage.

So given `my_number_map`, imagine we wanted the default value for any given key to be `0`. We can build a function like this:

```rust
#![cfg_attr(not(feature = "std"), no_std)]

use ink_lang as ink;

#[ink::contract]
mod mycontract {

    #[ink(storage)]
    pub struct MyContract {
        // Store a mapping from AccountIds to a u32
        my_number_map: ink_storage::collections::HashMap<AccountId, u32>,
    }

    impl MyContract {
        /// Private function.
        /// Returns the number for an AccountId or 0 if it is not set.
        fn my_number_or_zero(&self, of: &AccountId) -> u32 {
            let balance = self.my_number_map.get(of).unwrap_or(&0);
            *balance
        }
    }
}
```

Here we see that after we `get` the value from `my_number_map` we call `unwrap_or` which will either `unwrap` the value stored in storage, _or_ if there is no value, return some known value. Then, when building functions that interact with this HashMap, you need to always remember to call this function rather than getting the value directly from storage.

Here is an example:

```rust
#![cfg_attr(not(feature = "std"), no_std)]

use ink_lang as ink;

#[ink::contract]
mod mycontract {

    #[ink(storage)]
    pub struct MyContract {
        // Store a mapping from AccountIds to a u32
        my_number_map: ink_storage::collections::HashMap<AccountId, u32>,
    }

    impl MyContract {
        // Get the value for a given AccountId
        #[ink(message)]
        pub fn get(&self, of: AccountId) -> u32 {
            self.my_number_or_zero(&of)
        }

        // Get the value for the calling AccountId
        #[ink(message)]
        pub fn get_my_number(&self) -> u32 {
            let caller = self.env().caller();
            self.my_number_or_zero(&caller)
        }

        // Returns the number for an AccountId or 0 if it is not set.
        fn my_number_or_zero(&self, of: &AccountId) -> u32 {
            let value = self.my_number_map.get(of).unwrap_or(&0);
            *value
        }
    }
}
```

### Contract Caller <a id="contract-caller"></a>

As you might have noticed in the example above, we use a special function called `self.env().caller()`. This function is available throughout the contract logic and will always return to you the contract caller.

> **NOTE:** The contract caller is not the same as the origin caller. If a user triggers a contract which then calls a subsequent contract, the `self.env().caller()` in the second contract will be the address of the first contract, not the original user.

`self.env().caller()` can be used a number of different ways. In the examples above, we are basically creating an "access control" layer which allows a user to modify their own value, but no one else. You can also do things like define a contract owner during contract deployment:

```rust
#![cfg_attr(not(feature = "std"), no_std)]

use ink_lang as ink;

#[ink::contract]
mod mycontract {

    #[ink(storage)]
    pub struct MyContract {
        // Store a contract owner
        owner: AccountId,
    }

    impl MyContract {
        #[ink(constructor)]
        pub fn new(init_value: i32) -> Self {
            Self {
                owner: Self::env().caller();
            }
        }
        /* --snip-- */
    }
}
```

Then you can write permissioned functions which checks that the current caller is the owner of the contract.

### Your Turn! <a id="your-turn"></a>

Follow the `ACTION`s in the template code to introduce a storage map to your contract.

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
        // ACTION: Add a `HashMap` from `AccountId` to `u64` named `my_value`
    }

    impl Incrementer {
        #[ink(constructor)]
        pub fn new(init_value: i32) -> Self {
            Self {
                value: init_value,
            }
        }

        #[ink(constructor)]
        pub fn default() -> Self {
            Self {
                value: 0,
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
            // ACTION: Get `my_value` using `my_value_or_zero` on `&self.env().caller()`
            // ACTION: Return `my_value`
        }

        fn my_value_or_zero(&self, of: &AccountId) -> u64 {
            // ACTION: `get` and return the value of `of` and `unwrap_or` return 0
        }
    }

    #[cfg(test)]
    mod tests {
        use super::*;

        // Alias `ink_lang` so we can use `ink::test`.
        use ink_lang as ink;

        #[test]
        fn default_works() {
            let contract = Incrementer::default();
            assert_eq!(contract.get(), 0);
        }

        #[test]
        fn it_works() {
            let mut contract = Incrementer::new(42);
            assert_eq!(contract.get(), 42);
            contract.inc(5);
            assert_eq!(contract.get(), 47);
            contract.inc(-50);
            assert_eq!(contract.get(), -3);
        }

        // Use `ink::test` to initialize accounts.
        #[ink::test]
        fn my_value_works() {
            let contract = Incrementer::new(11);
            assert_eq!(contract.get(), 11);
            assert_eq!(contract.get_mine(), 0);
        }
    }
}
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

        fn my_value_or_zero(&self, of: &AccountId) -> u64 {
            *self.my_value.get(of).unwrap_or(&0)
        }
    }

    #[cfg(test)]
    mod tests {
        use super::*;

        use ink_lang as ink;

        #[test]
        fn default_works() {
            let contract = Incrementer::default();
            assert_eq!(contract.get(), 0);
        }

        #[test]
        fn it_works() {
            let mut contract = Incrementer::new(42);
            assert_eq!(contract.get(), 42);
            contract.inc(5);
            assert_eq!(contract.get(), 47);
            contract.inc(-50);
            assert_eq!(contract.get(), -3);
        }

        #[ink::test]
        fn my_value_works() {
            let contract = Incrementer::new(11);
            assert_eq!(contract.get(), 11);
            assert_eq!(contract.get_mine(), 0);
        }
    }
}
```
{% endtab %}
{% endtabs %}

