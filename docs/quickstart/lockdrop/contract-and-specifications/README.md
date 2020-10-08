# Contract  & Specifications

The lockdrop contract is a simple two function smart contract. When the function lock is called with the interface specified below via the Master Contract Lockdrop, a new Lockdrop User Contract is created that holds the timelocked ETH. Note, when `isValidator` is yes, the total allocated EDG may be staked at the time of distribution.

Notably, the Master Lockdrop Contract \(MLC\) itself does not hold the totality of locked ETH, instead, when calling lock, an individual Lockdrop User Contract \(LUC\) is created which holds the participant’s time-locked ETH. This 2-step arrangement reduces the potential value and feasibility of a malicious attack. Further, the Master Lockdrop and Lockdrop User Contracts are extremely simple.

In particular, the LUC contract is forty-five instructions until completing the call with no jumps. These have been audited by a third-party, Quantstamp.

## Lockdrop Participation

The Master Lockdrop Contract will accept ”locks” and ”signals” for a ninetyday Contribution Period. On Edgeware, lock interactions may have a duration of three months, six months, or 12 months with bonuses of 0%, 30%, and 120% respectively. In order to reduce centralization of power on Edgeware and increase the diversity of stakeholder voice, no single contributing ETH address or receiving EDG address will be able to obtain greater than or equal to 20% of the total EDG minted through the Lockdrop.

