# Getting a Value

Now that we have created and initialized a storage value, we are going to start to interact with it!

## Contract Functions <a id="contract-functions"></a>

As you can see in the contract template, all of your contract functions are part of your contract module.

```rust
impl MyContract {
    // Public and Private functions can go here
}
```

### Public and Private Functions <a id="public-and-private-functions"></a>

In Rust, you can make as many implementations as you want. As a stylistic choice, we recommend breaking up your implementation definitions for your private and public functions:

```rust
impl MyContract {
    /// Public function
    #[ink(message)]
    pub fn my_public_function(&self) {
        /* --snip-- */
    }

    /// Private function
    fn my_private_function(&self) {
        /* --snip-- */
    }

    /* --snip-- */
}
```

You can also choose to split things up however is most clear for your project.

Note that all public functions must use the `#[ink(message)]` attribute.

## Storage Value API <a id="storage-value-api"></a>

Without going into so much detail, storage values are a part of the underlying ink! core layer. In the background, they use a more primitive `cell` type which holds an `Option<T>`. When we try to get the value from storage, we `unwrap` the value, which is why it panics if it is not initialized!

```rust
impl<T> Value<T>
where
    T: scale::Codec,
{
    /// Returns an immutable reference to the wrapped value.
    pub fn get(&self) -> &T {
        self.cell.get().unwrap()
    }

    /// Returns a mutable reference to the wrapped value.
    pub fn get_mut(&mut self) -> &mut T {
        self.cell.get_mut().unwrap()
    }

    /// Sets the wrapped value to the given value.
    pub fn set(&mut self, val: T) {
        self.cell.set(val);
    }
}
```

In that same file, you can find the other APIs exposed by storage values, however these three are the most commonly used.

## Getting a Value <a id="getting-a-value-1"></a>

We already showed you how to initialize a storage value. Getting the value is just as simple:

```rust
impl MyContract {
    #[ink(message)]
    fn my_getter(&self) -> u32 {
        self.number
    }
}
```

In Rust, if the last expression in a function does not have a semicolon, then it will be the return value.

## Your Turn! <a id="your-turn"></a>

Follow the `ACTION`s on the code template provided.

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
    }

    impl Incrementer {
        #[ink(constructor)]
        pub fn new(init_value: i32) -> Self {
            Self {
                value: init_value
            }
        }

        #[ink(constructor)]
        pub fn default() -> Self {
            Self {
                value: 0
            }
        }

        #[ink(message)]
        // ACTION: Update this function to return an i32.
        pub fn get(&self) {
            // ACTION: Return the `value`.
        }
    }

    #[cfg(test)]
    mod tests {
        use super::*;

        #[test]
        fn default_works() {
            let contract = Incrementer::default();
            assert_eq!(contract.get(), 0);
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
                value: init_value
            }
        }

        #[ink(constructor)]
        pub fn default() -> Self {
            Self {
                value: 0
            }
        }

        #[ink(message)]
        pub fn get(&self) -> i32 {
            self.value
        }
    }

    #[cfg(test)]
    mod tests {
        use super::*;

        #[test]
        fn default_works() {
            let contract = Incrementer::default();
            assert_eq!(contract.get(), 0);
        }
    }
}
```
{% endtab %}
{% endtabs %}

