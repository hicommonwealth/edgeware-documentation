# Collection and Traits

In this part, we will be using the structs built previously and write public functions to add and fetch data from our contract.

## Collections <a id="collections"></a>

For this contract, we are going to store our voters in a HashMap with `AccountId` as a key and `Voter` instance as value. The HashMap can be imported from the `ink_storage` crate by:

```rust
use ink_storage::collections::HashMap;
```

The proposals will be stored in a `Vec` collection that can be imported from the `ink_prelude` crate. `ink_prelude` is a collection of data structures that operate on contract memory during contract execution. The vector can be imported by:

```rust
    use ink_prelude::vec::Vec;
```

Vectors can be instantiated in the same way as a HashMap. New objects can be added or referenced to from a vector using:

```rust
    let proposals: Vec<proposals> = Vec::new();
    // adding a new proposal
    proposals.push(
        Proposal{
            name:String::from("Proposal # 1"),
            vote_count: 0,
        });
    // returns the proposal at index 0 if exists else returns None
    let proposal = self.proposals.get(0).unwrap();
```

Remember that the `vector.get` returns an `Option` not the actual object!

## Traits <a id="traits"></a>

A trait tells the Rust compiler about the functionality a particular type has, and can be shared with other types. You can read more about them [here](https://doc.rust-lang.org/book/ch10-02-traits.html). Before using the custom built structures inside the `Ballot` storage, certain traits are required to be implemented for `Voter` and `Proposal` structs. These traits include:

* `Debug`: Allows debug formatting in format strings
* `Clone` : This trait allows you to create a deep copy of object
* `Copy` : The copy traits allows you to copy a value of a field
* `PackedLayout`: Types that can be stored to and loaded from a single contract storage cell
* `SpreadLayout`: Types that can be stored to and loaded from the contract storage.

You can learn more about these traits over [here](https://doc.rust-lang.org/book/appendix-03-derivable-traits.html) and [here](https://paritytech.github.io/ink/ink_storage/traits/index.html). These traits are implemented using the `derive` attribute:

```rust
    #[derive(Clone, Copy, Debug, scale::Encode, scale::Decode, SpreadLayout, PackedLayout, scale_info::TypeInfo)]
    struct XYZ {
        ...
        ...
    }
```

## Your Turn! <a id="your-turn"></a>

You need to:

* Create a proposal Vec and voters HashMap in Ballot struct.
* Update the constructor, so that it initializes a Vec of proposals and a HashMap of voters. Also update the voters HashMap to include the chair person as a voter.
* Create getters for both storage items.
* Write `add_voter` function to create a voter by the given `AccountId` and insert it in the HashMap of voters.
* Write `add_proposal` function that creates a `Proposal` object and inserts it tot he vector of proposals.

Remember to run `cargo +nightly test` to test your work.

{% tabs %}
{% tab title="🔨Starting Point" %}
```rust
#![cfg_attr(not(feature = "std"), no_std)]

use ink_lang as ink;

#[ink::contract]    
mod ballot {
    use ink_storage::collections::HashMap;
    use ink_prelude::vec::Vec;
    use ink_storage::traits::{PackedLayout, SpreadLayout};

    // Structure to store Proposal information
    #[derive(Clone, Debug, scale::Encode, scale::Decode, SpreadLayout, PackedLayout,scale_info::TypeInfo)]
    struct Proposal {
        name: String,
        vote_count: u32, 
    }

    // Structure to store Proposal information
    #[derive(Clone, Debug, scale::Encode, scale::Decode, SpreadLayout, PackedLayout,scale_info::TypeInfo)]
    pub struct Voter {
        weight: u32,
        voted: bool,
        delegate: Option<AccountId>, 
        vote: Option<i32>, 
    }

    /// Defines the storage of your contract.
    /// Add new fields the struct in order
    /// to add new static storage fields to your contract.
    #[ink(storage)]
    pub struct Ballot {
        chair_person: AccountId,
        //  ACTION: create a voters hash map with account id as key and Voter as value
        voters: 

        //  ACTION: create a proposals vector
        proposals: 
    }

    impl Ballot {
        #[ink(constructor)]
        pub fn new() -> Self {
            // get chair person address
            let chair_person =  Self::env().caller();

            //  ACTION: create empty proposals and voters variables
            //          * let proposals = 
            //          * let mut voters =

            // ACTION: add chair persons voter object in voters hash map
            // HINT: Use hashmap.insert(key,value)

            Self {
                chair_person,
                voters,
                proposals,
            }
        }

        // return chair person id
        #[ink(message)]
        pub fn get_chairperson(&self) -> AccountId {
            self.chair_person
        }

        // return the provided voter object
        pub fn get_voter(&self, voter_id: AccountId) -> Option<&Voter>{
        }

        // return the count of voters
        pub fn get_voter_count(&self) -> usize{
        }


        /// the function adds the provided voter id into possible
        /// list of voters. By default the voter has no voting right,
        /// the contract owner must approve the voter before he can cast a vote
        #[ink(message)]
        pub fn add_voter(&mut self, voter_id: AccountId) -> bool{
            // ACTION: check if voter already exits, if yes return false       
            //      * if not exists, create an entry in hash map 
            //      * with default weight set to 0 and voted to false
            //      * and return true

            // HINT: use hashmap.get() to get voter
            //        and use options.some() to check if voter exists
        }

        /// given an index returns the name of the proposal at that index
        pub fn get_proposal_name_at_index(&self, index:usize) -> &String {
        }

        /// returns the number of proposals in ballet
        pub fn get_proposal_count(&self) -> usize {
        }


        /// adds the given proposal name in ballet
        pub fn add_proposal(&mut self, proposal_name: String){
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
            let mut proposal_names: Vec<String> = Vec::new();
            proposal_names.push(String::from("Proposal # 1"));  
            let ballot = Ballot::new();
            assert_eq!(ballot.get_voter_count(),1);
        }

        #[ink::test]
        fn adding_proposals_works() {
            let mut ballot = Ballot::new();
            ballot.add_proposal(String::from("Proposal #1"));
            assert_eq!(ballot.get_proposal_count(),1);
        }

        #[ink::test]
        fn adding_voters_work() {
            let mut ballot = Ballot::new();
            let account_id = AccountId::from([0x0; 32]);
            assert_eq!(ballot.add_voter(account_id),true);
            assert_eq!(ballot.add_voter(account_id),false);
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
mod ballot {
    // use Hash
    use ink_storage::collections::HashMap;
    use ink_prelude::vec::Vec;
    use ink_storage::traits::{PackedLayout, SpreadLayout};

    // Structure to store Proposal information
    #[derive(Clone, Debug, scale::Encode, scale::Decode, SpreadLayout, PackedLayout,scale_info::TypeInfo)]
    struct Proposal {
        name: String,
        vote_count: u32, 
    }

    // Structure to store Proposal information
    #[derive(Clone, Debug, scale::Encode, scale::Decode, SpreadLayout, PackedLayout,scale_info::TypeInfo)]
    pub struct Voter {
        weight: u32,
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
        voters: HashMap<AccountId, Voter>,
        proposals: Vec<Proposal>    
    }

    impl Ballot {
        #[ink(constructor)]
        pub fn new() -> Self {
            // get chair person address
            let chair_person =  Self::env().caller();

            // create empty propsal and voters
            let proposals: Vec<Proposal> = Vec::new();
            let mut voters = HashMap::new();

            // initialize chair person's vote
            voters.insert(chair_person, Voter{
                weight:1,
                voted:false,
                delegate: None,
                vote: None,
            });

            Self {
                chair_person,
                voters,
                proposals,
            }
        }


        #[ink(message)]
        pub fn get_chairperson(&self) -> AccountId {
            self.chair_person
        }



        pub fn get_voter(&self, voter_id: AccountId) -> Option<&Voter>{
            self.voters.get(&voter_id)
        }

        pub fn get_voter_count(&self) -> usize{
            self.voters.len() as usize
        }

                /// the function adds the provided voter id into possible
        /// list of voters. By default the voter has no voting right,
        /// the contract owner must approve the voter before he can cast a vote
        #[ink(message)]
        pub fn add_voter(&mut self, voter_id: AccountId) -> bool{

            let voter_opt = self.voters.get(&voter_id);
            // the voter does not exists
            if voter_opt.is_some() {
                return false
            }

            self.voters.insert(voter_id, Voter{
                weight:0,
                voted:false,
                delegate: None,
                vote: None,
            });
            return true
        }



        /// given an index returns the name of the proposal at that index
        pub fn get_proposal_name_at_index(&self, index:usize) -> &String {
            let proposal = self.proposals.get(index).unwrap();
            return &proposal.name
        }

        /// returns the number of proposals in ballet
        pub fn get_proposal_count(&self) -> usize {
            return self.proposals.len()
        }

        /// adds the given proposal name in ballet
        /// to do: check unqiueness of proposal,
        pub fn add_proposal(&mut self, proposal_name: String){
            self.proposals.push(
                Proposal{
                    name:String::from(proposal_name),
                    vote_count: 0,
            });
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
            let mut proposal_names: Vec<String> = Vec::new();
            proposal_names.push(String::from("Proposal # 1"));  
            let ballot = Ballot::new();
            assert_eq!(ballot.get_voter_count(),1);
        }
    }

}
```
{% endtab %}
{% endtabs %}

