# FAQs for New Users

## Accounts & Balances

### I can't find my account using my public address in a block explorer.

Most block explorers require the version of the Edgeware Public Address that encodes the Edgeware Network ID - if you created your key/address in the Lockdrop or via the Polkadot UI or extension, you first need to regenerate your address using a program called Subkey before you can use it to search. Yu can always use your seed to connect to wallet services, regardless of the network ID. 

{% page-ref page="../accounts/regenerating-keys-with-edgeware-network-id.md" %}

### I'm seeing two different addresses depending on what service I use.

Edgeware accounts may have two address forms - one that encodes a Substrate Default Network ID and one that encodes the Edgeware network ID. Using block explorers, you should use the Edgeware form, and for all other cases we recommend the Edgeware network ID form, regenerate yours by following these instructions:

{% page-ref page="../accounts/regenerating-keys-with-edgeware-network-id.md" %}



## EDG Token

### Where can I buy or acquire EDG? Is it listed?

At this time, there are several low liquidity markets \(~150$ daily volume\) that list EDG. You should examine the security of these exchanges before making any purchases. Never buy seed phrases directly, your funds can be stolen. 

## Staking, Validation and Nomination

### Can I start staking EDG?

Yes, Edgeware launched with a fully functional proof-of-stake nomination \(also known as delegation,\) and validation system. Any user that holds EDG can participate in securing the network and receiving benefits \(but also endure the risks of being slashed for a validators nonconformance.\)

### How long does it take a waiting validator to become active? Why don't my nominators get selected?

Validators are elected from a pool of the top 60 most-bonded validators. This election method is not based on amount alone, but a complex algorithm called the Phragmen Method.

{% page-ref page="../staking/the-sequential-phragmen-method.md" %}

### **When can I unbond my nominated tokens?**

Bonding periods last 7 days.

### Why can't I send/sign my Nomination transaction? 

* Check that the Controller account has funds to pay transaction fees, this is the most common reason for issues. **If you get this error**: `staking.nominate`

  `submitAndWatchExtrinsic(extrinsic: Extrinsic): ExtrinsicStatus:: 1010: Invalid Transaction: Payment`

* Check that your Destination field in the Polkadot UI is set to the network default - and not to Kusama or other networks. 

### Why is it recommended to use a different account for Stash and Controller?

Separation of roles helps understand what accounts are performing what transactions, and allows us to disconnect the stash for security - making our wallets 'colder.' while still authorizing a controller to perform certain actions. You dont have to do this, but it is recommended.



### How often do I receive a reward from Staking?

Every 'era,' which is roughly  6 hours. An era is a category of block time.  [See more about time.](https://docs.edgewa.re/understanding-edgeware/network-parameters)



### How do I see my bonded versus frozen versus free balances in my accounts?

You can use the Polkadot UI, then click Chain State tab to query your account for various parameters.  

## Polkadot UI

### How do I connect to Edgeware Mainnet? OR I tried but it won't connect.

Click the network logo in the top right, and select Edgeware mainnet from the drop down. If you experience connection issues, try changing the endpoint using the custom endpoint option. See the following for other network endpoints:

{% page-ref page="../networks.md" %}

## Governance

## One-person-one vote - what will prevent malicious players from signing on multiple nodes if it will cost little?

We provide a variety of tallying rules for certain governance features on Edgeware. The core governance is run with coin-weighted voting, with extensions that mimic a form of quadratic voting based on locking time \(I.e you get more weight by locking longer\). Therefore what you ask is not wholly correct. Some tally types are inherently and unavoidably vulnerable to certain tactics- if someone wants to run a signaling poll with one person one vote that’s their decision, but we can provide guidance about results and process.

## 



