# Introduction to Edgeware Governance

 The core functionality of Edgeware’s governance is implemented in several extensible modules that users interact with to conduct governance: 

#### Signaling

 Non-binding polls are an important part of the governance process for existing blockchains. Users should also be able to create and distribute polls for signaling interest in different proposals, strategies, and directions. 

{% page-ref page="signaling-module.md" %}



#### Identity

 Edgeware requires a first-class identity primitive so people can identify each other in the governance process.

{% page-ref page="../identity-module/" %}



#### Democracy:

 The democracy module initially restricts votes on proposals to binary votes. This module allows for delegated voting–improving the total stake allocated towards a vote. Future upgrades should allows users to choose between many different methods for voting on a proposal \(e.g., binary or rank-choice\). 

{% page-ref page="democracy-voting-module.md" %}



#### Council: 

Edgeware allows voters to nominate a set of accounts that hold certain rights over the network. Council members can bias proposals. 

{% page-ref page="council/" %}



#### Treasury: 

This module allows individuals to vote on the allocation of a portion of newly minted EDG.

{% page-ref page="treasury.md" %}



