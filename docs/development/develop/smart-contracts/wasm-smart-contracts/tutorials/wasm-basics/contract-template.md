# Contract Template

Let's take a look at a high level what is available to you when developing a smart contract using the ink!.

## ink! <a id="ink"></a>

ink! is an [eDSL](https://wiki.haskell.org/Embedded_domain_specific_language) to write WebAssembly based smart contracts in the Rust programming language.

ink! is just standard Rust in a well defined "contract format" with specialized `#[ink(...)]` attribute macros. These attribute macros tell ink! what the different parts of your Rust smart contract represent, and ultimately allows ink! to do all the magic needed to create Substrate compatible Wasm bytecodes!

## Your Turn! <a id="your-turn"></a>

We are going to start a new project for the Incrementer contract we will build in this chapter.

So go into your working directory and run:

```text
cargo contract new incrementer
```

Just like before, this will create a new project folder named `incrementer` which we will use for the rest of this chapter.

```text
cd incrementer/
```

In the `lib.rs` file, replace the "Flipper" contract source code with the template code provided here.

Quickly check that it compiles and the trivial test passes with:

```text
cargo +nightly test
```

Also check that you can build the Wasm file by running:

```text
cargo +nightly contract build
```

If everything looks good, then we are ready to start programming!

{% tabs %}
{% tab title="✅Potential Solution" %}
{% code title="lib.rs" %}
```rust
#![cfg_attr(not(feature = "std"), no_std)]

use ink_lang as ink;

#[ink::contract]
mod incrementer {

    #[ink(storage)]
    pub struct Incrementer {
        // Storage Declaration
    }

    impl Incrementer {
        #[ink(constructor)]
        pub fn new(init_value: i32) -> Self {
            // Contract Constructor
            Self{}
        }

        #[ink(message)]
        pub fn get(&self) {
            // Contract Message
        }
    }

    #[cfg(test)]
    mod tests {
        #[test]
        fn default_works() {
            // Test Your Contract
        }
    }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

