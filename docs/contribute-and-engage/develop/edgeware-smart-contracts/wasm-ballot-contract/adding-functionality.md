# Adding Functionality

In this part we will add functionality to our Ballot so that:

* People can vote on proposals
* People can delegate their votes
* The chairperson can assign voting rights

### Contract Functionality <a id="contract-functionality"></a>

**Constructor:**

Let's first update the constructor of our contract. As you can see in the code sample on the right, the constructor now accepts a `Option<Vector<String>>` parameter. The constructor expects a vector of strings as input. We need to update the constructor so that the provided proposal names are used to create the `Proposal` objects and added to our ballot storage. To check if the vector containing strings is provided:

```rust
    if proposal_name.is_some() {
        names = proposal_name.unwrap()
        // do somethiing with names 

    }
```

**Give Voting Right:**

In the previous part we created a function that allowed users to add themselves as a voter. We initialized their voter struct with `voter.weight=0` because when a voter is created, he/she has no voting right by default. So, let's create a function `give_voting_right` that will only allow the chairperson to update the weight to 1 for any given voter. The function will look something like:

```rust
    // assuming that the caller is the chair person
    pub fn give_voting_right(&mut self, voter_id: AccountId) {
        let voter_opt = self.voters.get_mut(&voter_id);
        if voter_opt.is_some() {
            let voter = voter.unwrap()
            // assuming that the voter has not already voted
            voter.weight = 1
        }
    }
```

**Vote:**

Now, let's implement a function that will allow users to cast their votes. This function will take a proposal index as input. If the `caller` is a valid voter and has not already casted his/her vote, update the proposal at index `i` with the weight of the voter, update `voter.voted` to true and set `voter.vote` to index `i`.

**Get Winning Proposal:**

Now that the votes are cast, we will implement a function that will get the name of the winning proposal. In a recall election, the winner is announced once the voting time has passed out. We will leave such implementation to you. For now, we will allow any user to invoke this function and get the name of the winning proposal. Let's implement a function to return the index of the proposal with the maximum votes:

```rust
    fn winning_proposal(&self) -> Option<usize> {
        let mut winning_vote_vount:u32 = 0;
        let mut winning_index: Option<usize> = None;
        let mut index: usize = 0;

        for val in self.proposals.iter() {
            if val.vote_count > winning_vote_vount {
                winning_vote_vount = val.vote_count;
                winning_index = Some(index);
            }
            index += 1

        }
        return winning_index
    }
```

Notice that this function returns `Option<usize>`, not `usize`, since it's possible that there are no proposals in the ballot. This function can be used to find the name of winning proposal.

**Delegation:**

In our voter struct, there is a `delegate` field defined as `Option<AccountId>` to allow voters to delegate their vote to someone else. This can be achieved using the following function:

```rust
    #[ink(message)]
    pub fn delegate(&mut self, to: AccountId)  {

        // account id of the person who invoked the function
        let sender_id = self.env().caller();
        let sender_weight;
        // self delegation is not allowd
        assert_ne!(to,sender_id, "Self-delegation is disallowed.");

        {
            let sender_opt =  self.voters.get_mut(&sender_id);
            // the voter invoking the function should exist in our ballot
            assert_eq!(sender_opt.is_some(),true, "Caller is not a valid voter");
            let sender = sender_opt.unwrap();

            // the voter must not have already casted their vote
            assert_eq!(sender.voted,false, "You have already voted");

            sender.voted = true;
            sender.delegate = Some(to);
            sender_weight = sender.weight;
        }

        {
            let delegate_opt = self.voters.get_mut(&to);
            // the person to whom the vote is being delegated must be a valid voter
            assert_eq!(delegate_opt.is_some(),true, "The delegated address is not valid");

            let delegate = delegate_opt.unwrap();

            // the voter should not have already voted
            if delegate.voted {
                // If the delegate already voted,
                // directly add to the number of votes
                let voted_to = delegate.vote.unwrap() as usize;
                self.proposals[voted_to].vote_count += sender_weight;
            } else {
                // If the delegate did not vote yet,
                // add to her weight.
                delegate.weight += sender_weight;
            }
        }
    }
```

You will see that in the delegation function above, we update the `sender.voted` and `sender.delegate` fields prior to checking if the person being delegated is a valid voter. The function will panic if the delegated person is not a valid voter and will roll back the changes made to the `sender.voted` and `sender.delegate` fields.

## Your Turn! <a id="your-turn"></a>

This wraps up the tutorial. Practice what you learned with the following exercises:

* Update the `constructor` function so that if a vector of proposal names is provided, a new proposal object is created and added to `ballot.proposal`.
* Define the `give_voting_right` function as instructed.
* Add `vote` functionality and update the ballot according to the template requirements.
* Update `get_winning_proposal_name` functionality to return the name of the winning proposal.

{% tabs %}
{% tab title="🔨Starting Point" %}
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
        pub fn new(proposal_names: Option<Vec<String>> ) -> Self {

            // get chair person address
            let chair_person =  Self::env().caller();

            // create empty propsal and voters
            let mut proposals: Vec<Proposal> = Vec::new();
            let mut voters = HashMap::new();

            // initialize chair person's vote
            voters.insert(chair_person, Voter{
                weight:1,
                voted:false,
                delegate: None,
                vote: None,
            });


            // ACTION : Check if proposal names are provided.
            //        * If yes then create and push proposal objects to proposals vector


            Self {
                chair_person,
                voters,
                proposals,
            }
        }

        /// default constrcutor
        #[ink(constructor)]
        pub fn default() -> Self {
            Self::new(Default::default())
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

        /// Give `voter` the right to vote on this ballot.
        /// Should only be called by `chairperson`.
        #[ink(message)]
        pub fn give_voting_right(&mut self, voter_id: AccountId) {
            let caller = self.env().caller();
            let voter_opt = self.voters.get_mut(&voter_id);
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
        pub fn new(proposal_names: Option<Vec<String>> ) -> Self {

            // get chair person address
            let chair_person =  Self::env().caller();

            // create empty propsal and voters
            let mut proposals: Vec<Proposal> = Vec::new();
            let mut voters = HashMap::new();

            // initialize chair person's vote
            voters.insert(chair_person, Voter{
                weight:1,
                voted:false,
                delegate: None,
                vote: None,
            });


            // ACTION : Check if proposal names are provided.
            //        * If yes then create and push proposal objects to proposals vector
            // if proposals are provided
            if proposal_names.is_some() {
                // store the provided propsal names
                let names = proposal_names.unwrap();
                for name in &names {
                    proposals.push(
                        Proposal{
                        name: String::from(name),
                        vote_count: 0,
                    });
                }
            }

            Self {
                chair_person,
                voters,
                proposals,
            }
        }

        /// default constrcutor
        #[ink(constructor)]
        pub fn default() -> Self {
            Self::new(Default::default())
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
```
{% endtab %}
{% endtabs %}

