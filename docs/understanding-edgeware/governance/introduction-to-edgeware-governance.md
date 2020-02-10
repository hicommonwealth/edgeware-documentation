# Edgeware Governance

## Edgeware Governance

The original governance of Edgeware is composed of two bodies:

1\) **The Referendum Chamber** - The broadest and most powerful body of Edgeware governance. It is composed of an assembly of all EDG holders, weighted by amount of tokens held and voluntary [lock-commitment](https://wiki.polkadot.network/en/latest/polkadot/node/governance/#voluntary-locking).   
  
2\) **The Council** - Members of this body are elected through [approval voting](https://wiki.polkadot.network/en/latest/polkadot/node/governance/#how-to-be-a-council-member) of EDG holders, weighted by the number of tokens controlled. 

  
The core functionality of Edgeware’s governance, and the tools of these two bodies, is implemented in several extensible modules that users interact with to conduct governance.

## Modules

### Signaling

Non-binding polls are an important part of the governance process for existing blockchains. Users should also be able to create and distribute polls for signaling interest in different proposals, strategies, and directions. 

{% page-ref page="signaling-module.md" %}



### Identity

 Edgeware requires a first-class identity primitive so people can identify each other in the governance process.

{% page-ref page="../identity-module/" %}



### Democracy

The democracy module initially restricts votes on proposals to binary votes. This module allows for delegated voting–improving the total stake allocated towards a vote. Future upgrades should allows users to choose between many different methods for voting on a proposal \(e.g., binary or rank-choice\). 

{% page-ref page="democracy-voting-module/" %}



### Council

Edgeware allows voters to nominate a set of accounts that hold certain rights over the network. Council members can bias proposals. 

{% page-ref page="council/" %}



### Treasury

This module allows individuals to vote on the allocation of a portion of newly minted EDG.

{% page-ref page="treasury/" %}



## Participating in Edgeware Governance

You can participate in Edgeware governance by making proposals, voting on referenda, and voting for council members. Edgeware currently has a basic governance UI, found at both[ Commonwealth.im/Edgeware](https://commonwealth.im/edgeware) at [polkadot.js.org/apps/\#/democracy](https://polkadot.js.org/apps/#/democracy). You will need EDG to participate in Edgeware governance.

#### Public Discussion[¶](https://guide.kusama.network/en/latest/try/governance/#public-discussion) <a id="public-discussion"></a>

Discuss governance proposals on the [Discussions tab at Commonwealth.im/Edgeware](https://commonwealth.im/edgeware)

### 

### Next..

{% page-ref page="democracy-voting-module/view-and-vote-on-referenda.md" %}

{% page-ref page="council/voting-for-council.md" %}

{% page-ref page="council/run-for-council.md" %}



