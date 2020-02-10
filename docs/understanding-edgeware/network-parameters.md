---
description: >-
  This page is intended to list the current network parameter configurations.
  These are liable to change through governance processes, and can be double
  checked using the instructions below.
---

# Parameters

## Accounts and Transactions

| **Parameter** | Value | Description |
| :--- | :--- | :--- |
| **Reaping Threshold** | 0.001 EDG | The minimum EDG required in the account balance to create or maintain an account. |
| **Transaction Minimum** | ??? | The Min. amount you can send to an Edgeware Address. |

## Consensus

| Parameter | Value |
| :--- | :--- |
| **Runtime Version** | 28 |
| **Consensus Mechanism** | AURA |
| **Finality Gadget** | GRANDPA |

## Time

| Edgeware | Time | Slots\* |
| :--- | :--- | :--- |
| **Block** | 6 seconds | 1 |
| **Epoch** | 60 minutes | 600 |
| **Session** | 60 minutes \(600 Blocks\) | 600 |
| **Era** | 6 hours \(6 sessions\) | 3600 |

## Staking 

| **Parameter** | Value |
| :--- | :--- |
| **Validator Slots** | 60 |
| **Validator Bonding Duration** | 7 days |
| **Slash Deferral Duration** | 7 days |
| **Slash Cancellation Vote** | Requires 3/4 of Council to Approve |

## Democracy \(Referenda\) 

| Parameter | Value |
| :--- | :--- |
| **Launch Period** | 7 days |
| **Voting Period** | 7 days |
| **Enactment Delay** | 10 days |
| **Passing Vote Criteria** | Supermajority to pass |
| **Fast Track Voting Period** | Not active |
| **Veto** | Not active |
| **Proposal Cancellation Vote** | Requires 2/3 of council to Approve Cancellation |
| **Cool-off Period after Proposal Cancellatio** | 7 days |
| **Min. EDG Deposit to Vote** | ??? |

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

| **Parameter** | Value | Description |
| :--- | :--- | :--- |
| **Term Duration** | 28 days | A new councilperson is elected every 28 days based on the Phragmen algorithm. If the term duration is changed the current term is affected when `BlockNumber % TermDuration ==0`, upon which a new council \(or councilperson?\) will be selected. |
| **Candidacy Bond** | 1000 EDG | The amount a user must bond to submit their candidacy. |
| **Voting Bond** | 10 EDG | The amount of EDG that a voter must lock to vote for Council. |
| **Council Member Slots** | 13 members | The size of the council. |
| **Runners-up Slots** | 7 members | The number of slots that will be displayed as a runner-up. |

## **Treasury** 

| **Parameter** | Value | Description |
| :--- | :--- | :--- |
| **Budgeting Period** |  7 days |  |
| **Proposal Bond** | 5% and minumum 1000 EDG | The amount required to bond in order to propose a treasury spend. If approved, it is returned, if the proposal fails, it is burnt.  |
| **Burn unspent treasury funds** | Off | This deactivates a burn of all  unspent treasury funds at the end of a budgeting period. |

## **Signaling** 

| Parameter | Value | Description |
| :--- | :--- | :--- |
| **Signaling Period** | 7 days | The length of time a signal proposal is active for engagement.  |
| **Signaling Proposal Bond** | 100 EDG | The amount of EDG required to bond to submit a signaling proposal.  |

## Identity

| Parameter | Value | Description |
| :--- | :--- | :--- |
| **Required Bond Per Identity**  | 10 EDG | Bond required to store IDs on-chain. |
| **Required Bond Per Each Additional Identity Field** | 2.5 EDG | Bond required to store **additional** IDs on-chain **Beyond Legal Name.** |
| **Sub-Account Deposit** | 2 EDG | Amount required to deposit in order to create a sub account. |
| **Maximum Sub-Accounts** | 100 | The maximum number of sub account an account may have. |

##  Economics

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Value (Units)</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>Minimum Inflation</b>
      </td>
      <td style="text-align:left">0_025_000</td>
      <td style="text-align:left">The min. inflation rate the system will permit.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Maximum Inflation</b>
      </td>
      <td style="text-align:left">
        <p>&lt;b&gt;&lt;/b&gt;</p>
        <p>0_100_000</p>
      </td>
      <td style="text-align:left">The max. inflation rate the system will permit.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Ideal Staking Rate</b>
      </td>
      <td style="text-align:left">
        <p>&lt;b&gt;&lt;/b&gt;</p>
        <p>0_800_000</p>
      </td>
      <td style="text-align:left">The ideal proportion of EDG tokens staked compared to total EDG supply.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Falloff Rate</b>
      </td>
      <td style="text-align:left">
        <p>&lt;b&gt;&lt;/b&gt;</p>
        <p>0_050_000,</p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Max Piece Count</b>
      </td>
      <td style="text-align:left">40</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Test Precision</b>
      </td>
      <td style="text-align:left">0_005_000</td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>## Contract configuration

| Parameter | Value | Description |
| :--- | :--- | :--- |
| **Contract Transfer Fee** | 0.10 EDG | \*\*\*\* |
| **Contract Creation Fee** | 0.10 EDG | \*\*\*\* |
| **Contract Transaction Base Fee** | 0.10 EDG | \*\*\*\* |
| **Contract Transaction Byte Fee** | 0.001 EDG | \*\*\*\* |
| **Contract Fee** | 0.10 EDG | \*\*\*\* |
| **Tombstone Deposit** | 1 EDG | \*\*\*\* |
| **Rent Byte Fee** | 1 EDG | \*\*\*\* |
| **Rent Deposit Offset** | 1000 EDG | \*\*\*\* |
| **Surcharge Reward** | 150 EDG |  |

## Genesis

| Parameter | Value |
| :--- | :--- |
| Council Members | 1 Member at time of Genesis \(Commonwealth Labs 0x02456...\) |
| Identity Attestation Provider | 1 Verifier at time of Genesis \(Commonwealth Labs 0x92c32...\) |

\*\*\*\*



