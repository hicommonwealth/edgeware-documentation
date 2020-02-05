# Nomination Period

Any potential validators can indicate their intention to be a validator candidate. Their candidacies are made public to all nominators, and a nominator in turn submits a list of any number of candidates that it supports. In the next epoch \(lasting several hours\), a certain number of validators having the most DOT backing get elected and become active. There are no particular requirements for a DOT holder to become a nominator, though we expect each nominator to carefully track the performance and reputation of validators.

Once the nomination period ends, the NPoS election mechanism takes the nominators and their associated votes as input, and outputs a set of validators of the required size, that maximizes the stake backing of any validator, and that makes the stakes backing validators as evenly distributed as possible. The objectives of this election mechanism are to maximize the security of the network, and achieve fair representation of the nominators. If you want to know more about how NPoS works \(e.g. election, running time complexity, etc.\), please read [here](http://research.web3.foundation/en/latest/polkadot/NPoS/).

