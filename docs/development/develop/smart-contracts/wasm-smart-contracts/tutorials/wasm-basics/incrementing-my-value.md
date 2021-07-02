# Storing a Value

The first thing we are going to do to the contract template is introduce some storage values.

Here is how you would store some simple values in storage:

```rust
#[ink(storage)]
pub struct MyContract {
    // Store a bool
    my_bool: bool,
    // Store some number
    my_number: u32,
}
/* --snip-- */
```

## Supported Types <a id="supported-types"></a>

Contract may store types that are encodable and decodable with [Parity Codec](https://github.com/paritytech/parity-codec) which includes the most common types such as `bool`, `u{8,16,32,64,128}`, `i{8,16,32,64,128}`, `String`, tuples, and arrays.

ink! provides smart contracts Substrate specific types like `AccountId`, `Balance`, and `Hash` as if they were primitive types. Also ink! provides storage types for more elaborate storage interactions through the storage module:

```rust
use ink_storage::collections::{Vec, HashMap, Stash, Bitvec};
```

Here is an example of how you would store an `AccountId` and `Balance`:

```rust
// We are importing the default ink! types
use ink_lang as ink;

#[ink::contract]
mod MyContract {

    // Our struct will use those default ink! types
    #[ink(storage)]
    pub struct MyContract {
        // Store some AccountId
        my_account: AccountId,
        // Store some Balance
        my_balance: Balance,
    }
    /* --snip-- */
}
```

You can find all the supported Substrate types in [`crates/storage/src/lib.rs`](https://github.com/paritytech/ink/blob/master/crates/storage/src/lib.rs).

## Contract Deployment <a id="contract-deployment"></a>

Every ink! smart contract must have a constructor which is run once when a contract is created. ink! smart contracts can have multiple constructors:

```rust
use ink_lang as ink;

#[ink::contract]
mod mycontract {

    #[ink(storage)]
    pub struct MyContract {
        number: u32,
    }

    impl MyContract {
        /// Constructor that initializes the `u32` value to the given `init_value`.
        #[ink(constructor)]
        pub fn new(init_value: u32) -> Self {
            Self {
                number: init_value,
            }
        }

        /// Constructor that initializes the `u32` value to the `u32` default.
        ///
        /// Constructors can delegate to other constructors.
        #[ink(constructor)]
        pub fn default() -> Self {
            Self {
                number: Default::default(),
            }
        }
    /* --snip-- */
    }
}
```

## [Your Turn!](https://contracts.edgewa.re/#/1/storing-a-value?id=your-turn) <a id="your-turn"></a>

Follow the `ACTION`s in the template.

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
        // ACTION: Create a storage value called `value` which holds a `i32`
    }

    impl Incrementer {
        #[ink(constructor)]
        pub fn new(init_value: i32) -> Self {
            // ACTION: Create a new `Incrementer` and set its `value` to `init_value`
        }

        // ACTION: Create a second constructor function named `default`.
        //         It has no input, and creates a new `Incrementer` with its `value`
        //         set to `0`.

        #[ink(message)]
        pub fn get(&self) {
            // Contract Message
        }
    }

    #[cfg(test)]
    mod tests {
        use super::*;

        #[test]
        fn default_works() {
            Incrementer::default();
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
        pub fn get(&self) {
            // Contract Message
        }
    }

    #[cfg(test)]
    mod tests {
        use super::*;

        #[test]
        fn default_works() {
            Incrementer::default();
        }
    }
}
```
{% endtab %}
{% endtabs %}

