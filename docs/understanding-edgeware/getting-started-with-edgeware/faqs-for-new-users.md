# FAQs for New Users

### Accounts & Balances

#### I can't find my account using my public address in a block explorer.

Most block explorers require the version of the Edgeware Public Address that encodes the Edgeware Network ID - if you created your key/address in the Lockdrop or via the Polkadot UI or extension, you first need to regenerate your address using a program called Subkey before you can use it to search. Yu can always use your seed to connect to wallet services, regardless of the network ID. 

{% page-ref page="../accounts/regenerating-keys-with-edgeware-network-id.md" %}



### EDG Token

#### Where can I buy or acquire EDG? Is it listed?

At this time, there are several low liquidity markets \(~150$ daily volume\) that list EDG. You should examine the security of these exchanges before making any purchases. Never buy seed phrases directly, your funds can be stolen. 





### Staking, Validation and Nomination

#### Can I start staking EDG?

Yes, Edgeware launched with a fully functional proof-of-stake nomination \(also known as delegation,\) and validation system. Any user that holds EDG can participate in securing the network and receiving benefits \(but also endure the risks of being slashed for a validators nonconformance.\)

#### How long does it take a waiting validator to become active? Why don't my nominators get selected?

Validators are elected from a pool of the top 60 most-bonded validators. This election method is not based on amount alone, but a complex algorithm called the Phragmen Method.

{% page-ref page="../nominated-proof-of-stake-npos/the-sequential-phragmen-method.md" %}



#### Why can't I send/sign my Nomination transaction?

* Check that the Controller account has funds to pay transaction fees, this is the most common reason for issues.
* Check that your Destination field in the Polkadot UI is set to the network default - and not to Kusama or other networks. 

