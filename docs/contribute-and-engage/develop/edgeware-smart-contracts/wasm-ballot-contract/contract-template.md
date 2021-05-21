# Contract Template

Let's start with making a new ink! project to build the ballot contract.

In your working directory, run:

```text
cargo contract new ballot
```

Replace the content of `lib.rs` file with the template on the right.

The contract storage consists of an `AccountId` which we initialize to the callers id in the constructor. There is a function `get_chair_person` implemented that returns the id of the the chair\_person\(owner\) of the contract.

## Struct <a id="struct"></a>

You may have come across the [struct](https://doc.rust-lang.org/book/ch05-01-defining-structs.html) keyword in previous tutorials, but so far we have used structs to define the storage of contracts. In this contract, we use it to define the following custom types that are going to be used later use as part ballot storage:

* `Proposal`: This struct stores information about a proposal. Each proposal contains:
  * `name`: A field to store the name of the proposal
  * `vote_count`: A 32 bit unsigned integer for storing the number of votes the proposal has received.
* `Voter`: For each voter in the system, we instantiate a voter struct with:
  * `weight`: An unsigned weight indicating the weightage of the voter. The weightage of a voter can vary based on election/network parameters.
  * `voted`: It is set to false by default, but once a voter has voted, it's set to true so that the same voter can not cast his vote again.
  * `delegate`: A voter can choose to delegate their vote to some one else. Since it's not necessary for voters to delegate, this field is created as an `Option`.
  * `vote`: Index of the proposal that the user has casted the vote to. This is created as an `Option` set to None by default.

Unlike our contract struct `Ballot` we don't use the macro `ink(storage)` for our custom defined structs as there can only be a single storage struct for a contract. Also, our structs are not public as users don't need to interact with them directly.

## Ink\_Prelude <a id="ink_prelude"></a>

`ink_pelude` crate provides data structures such as `HashMap`, `Vector` etc.. to operate on contract memory during contract execution. We will be importing these collections in next parts of this tutorial so before moving forward update contract's cargo.toml file with following dependency: `ink_prelude = { version = "3.0.0-rc2", default-features = false }`

## Compilaton and Warnings <a id="compilaton-and-warnings"></a>

You can build the contract using `cargo +nightly build` and run tests using `cargo +nightly test`. The contract will successfully compile and pass all tests, but the rust compiler will give you the following warnings:

```rust
warning: struct is never constructed: `Proposal`
  --> lib.rs:10:12
   |
10 |     struct Proposal {
   |            ^^^^^^^^
   |
   = note: `#[warn(dead_code)]` on by default

warning: struct is never constructed: `Voter`
  --> lib.rs:16:16
   |
16 |     pub struct Voter {
   |                ^^^^^

warning: 2 warnings emitted
```

This is because the structs we have defined are never used. We will get to that in next part!

{% tabs %}
{% tab title="🔨Starting Point" %}
```rust
#![cfg_attr(not(feature = "std"), no_std)]

use ink_lang as ink;

#[ink::contract]
mod ballot {
    // Structure to store Proposal information
    struct Proposal {
        name: String,
        vote_count: i32, 
    }

    // Structure to store Proposal information
    pub struct Voter {
        weight: i32,
        voted: bool,
        delegate: Option<AccountId>, 
        vote: Option<i32>, 
    }

    /// Defines the storage of your contract.
    /// Add new fields to the below struct in order
    /// to add new static storage fields to your contract.
    #[ink(storage)]
    pub struct Ballot {
        chair_person: AccountId,
    }

    impl Ballot {
        #[ink(constructor)]
        pub fn new() -> Self {
            let owner = Self::env().caller();
            Self { 
                chair_person:owner,
              }
        }


        #[ink(message)]
        pub fn get_chairperson(&self) -> AccountId {
            self.chair_person
        }

    }

    /// Unit tests in Rust are normally defined within such a `#[cfg(test)]`
    /// module and test functions are marked with a `#[test]` attribute.
    /// The below code is technically just normal Rust code.
    #[cfg(test)]
    mod tests {
        /// Imports all the definitions from the outer scope so we can use them here.
        use super::*;

        // Alias `ink_lang` so we can use `ink::test`.
        use ink_lang as ink;

        #[ink::test]
        fn new_works() {
            let ballot = Ballot::new();
            assert_eq!(ballot.get_chairperson(),AccountId::from([0x1; 32]));
        }
    }
}
```
{% endtab %}
{% endtabs %}

