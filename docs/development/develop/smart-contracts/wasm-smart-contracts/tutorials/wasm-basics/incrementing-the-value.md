# Incrementing the Value

It's time to let our users modify storage!

## Mutable and Immutable Functions <a id="mutable-and-immutable-functions"></a>

You may have noticed that the function templates included `self` as the first parameter of the contract functions. It is through `self` that you gain access to all your contract functions and storage items.

If you are simply _reading_ from the contract storage, you only need to pass `&self`. But if you want to _modify_ storage items, you will need to explicitly mark it as mutable, `&mut self`.

```rust
impl MyContract {
    #[ink(message)]
    pub fn my_getter(&self) -> u32 {
        self.my_number
    }

    #[ink(message)]
    pub fn my_setter(&mut self, new_value: u32) {
        self.my_number = new_value;
    }
}
```

## Lazy Storage Values <a id="lazy-storage-values"></a>

There is a `Lazy` type that can be used for ink! storage values that don't need to be loaded in some or most cases. Because they do not meet this criteria, many simple ink! examples, including those in this workshop, do not require the use `Lazy` values. Since there is some overhead associated with `Lazy` values, they should only be used where required.

```rust
#[ink(storage)]
pub struct MyContract {
    // Store some number
    my_number: ink_storage::Lazy<u32>,
}

impl MyContract {
    #[ink(constructor)]
    pub fn new(init_value: i32) -> Self {
        Self {
            my_number: Default::default(),
        }
    }

    #[ink(message)]
    pub fn my_setter(&mut self, new_value: u32) {
        ink_storage::Lazy::<u32>::set(&mut self.my_number, new_value);
    }

    #[ink(message)]
    pub fn my_adder(&mut self, add_value: u32) {
        let my_number = &mut self.my_number;
        let cur = ink_storage::Lazy::<u32>::get(my_number);
        ink_storage::Lazy::<u32>::set(my_number, cur + add_value);
    }
}
```

## Your Turn <a id="your-turn"></a>

Follow the `ACTION`s in the template code.

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
            // ACTION: Simply increment `value` by `by`
        }
    }

    #[cfg(test)]
    mod tests {
        use super::*;

        #[test]
        fn default_works() {
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
        pub fn get(&self) -> i32 {
            self.value
        }

        #[ink(message)]
        pub fn inc(&mut self, by: i32) {
            self.value += by;
        }
    }

    #[cfg(test)]
    mod tests {
        use super::*;

        #[test]
        fn default_works() {
```
{% endtab %}
{% endtabs %}

