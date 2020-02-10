---
description: >-
  This page is intended to list the current network parameter configurations.
  These are liable to change through governance processes, and can be double
  checked using the instructions below.
---

# Network Parameters

## Accounts and Transactions

**Reaping Threshold:** 0.001 EDG  
The minimum EDG required in the account balance to create or maintain an account.

**Transaction Minimum:**   
The minimum amount you can send to an Edgeware address

## Consensus and Time

**Runtime Version**: 28

**Consensus Mechanism:** AURA

**Finality Gadget:** GRANDPA

| Edgeware | Time | Slots\* |
| :--- | :--- | :--- |
| Block | 6 seconds | 1 |
| Epoch | 60 minutes | 600 |
| Session | 60 minutes \(600 Blocks\) | 600 |
| Era | 6 hours \(6 sessions\) | 3600 |

## Staking 

**Validator Slots:** 60

**Validator Bonding Duration**: 7 days

**Slash Deferral Duration:** 7 days

**Slash Cancellation Vote:** Requires 3/4 of Council to Approve

## Democracy \(Referenda / Proposals\) 

**Launch Period:** 7 Days  
The cycle on which a new referendum is selected by the system and raised for a vote.

**Voting Period:** 7 days  
The length of time the governing body has to vote on a referendum.

**Enactment Delay:** 10 days  
The length of time from the completion of a passing referendum to it's implementation in the system.

**Passing Vote Criteria:** Supermajority to Pass

**Fast Track Voting Period**: N/A, None Implemented

**Veto:** None implemented

**Proposal Cancellation Vote:** Requires 2/3 of council to Approve Cancellation

**Cool-off Period after Proposal Cancellation**: 7 Days

**Minimum EDG Deposit to Vote:** \_\_\_\_\_

**Vote Weighting by Lock Time**  
The schedule of weight boosts on a quadratic curve - meaning that exponentially increasing locktimes are required to achieve lesser proportional boosts in weight.

| Vote Weight | Locktime |
| :--- | :--- |
| 0.1x | None |
| 1x | 1x Enactment Period \(10 days\) |
| 2x | 2x Enactment Period \(20 days\) |
| 3x | 4x Enactment Period \(40 days\) |
| 4x | 8x Enactment Period \(80 days\) |
| 5x | 16x Enactment Period \(160 days\) |
| 6x | 32x Enactment Period \(320 days\) |

## Council Elections

**Term Duration:** 28 days  
A new councilperson is elected every 28 days based on the Phragmen algorithm. If the term duration is changed the current term is affected when `BlockNumber % TermDuration ==0`, upon which a new council \(or councilperson?\) will be selected.

**Candidacy Bond:** 1000 EDG  
The amount a user must bond to submit their candidacy.

**Voting Bond:** 10 EDG  
The amount of EDG that a voter must lock to vote for Council.

**Council Member Slots:** 13 members  
The size of the council.

**Runners-up slots:** 7 members  
The number of slots that will be displayed as a runner-up.

## **Treasury** 

**Budgeting period:** 7 days

**Proposal bond:** 5%, minimum 1000 EDG  
The amount required to bond in order to propose a treasury spend. If approved, it is returned, if the proposal fails, it is burnt. 

**Burn unspent treasury funds:** Off  
This deactivates a burn of all  unspent treasury funds at the end of a budgeting period.

## **Signaling** 

**Signaling period:** 7 days  
The length of time a signal proposal is active for engagement. 

**Proposal bond:** 100 EDG  
The amount of EDG required to bond to submit a proposal. 

## Identity

**Required Bond Per Identity** 10 EDG  
****Bond required to store IDs on-chain.

**Required Bond Per Each Additional Identity Field** 2.5 EDG  
****Bond required to store **additional** IDs on-chain **Beyond Legal Name.**

**Sub-Account Deposit: 2 EDG**

**Maximum Sub-Accounts: 100** 

##  Economics

#### Token Economics 

* **min\_inflation**: 0\_025\_000,
* **max\_inflation:** 0\_100\_000,
* **ideal\_stake**: 0\_800\_000,
* **falloff:** 0\_050\_000,
* **max\_piece\_count:** 40,
* **test\_precision:** 0\_005\_000,

## Contract configuration

* **Contract transfer fee:** .10 EDG
* **Contract creation fee:** .10 EDG
* **Contract transaction base fee:** .10 EDG 
* **Contract transaction byte fee:** .001 EDG
* **Contract fee:** .10 EDG 
* **Tombstone deposit:** 1 EDG
* **Rent byte fee:** 1 EDG
* **Rent deposit offset:** 1000 EDG
* **Surcharge reward:** 150 EDG

## Genesis

**Council:** 1 member at genesis \(0x02456...\)

**Commonwealth Social Attestation:** 1 verifier at genesis \(0x92c32...\)



