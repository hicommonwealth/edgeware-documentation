---
description: >-
  This page is intended to list the current network parameter configurations.
  These are liable to change through governance processes, and can be double
  checked using the instructions below.
---

# Parameters

{% hint style="info" %}
This page reflects the runtime [file of the chain viewable at Github](https://github.com/hicommonwealth/edgeware-node/blob/master/node/runtime/src/lib.rs), which is the final source of authority. You can also use the Polkadot.js apps to confirm the current value of these parameters on a testnet or mainnet at[ Chain State tab &gt; Constants &gt; Select Parameter](https://polkadot.js.org/apps/#/chainstate/constants)
{% endhint %}

## Accounts and Transactions

| **Parameter** | Value | Description |
| :--- | :--- | :--- |
| **Reaping Threshold** | 0.001 EDG | The minimum EDG required in the account balance to create or maintain an account. |
| **Transaction Minimum** | 1e-18 | The Min. amount you can send to an Edgeware Address. |

## Consensus

| Parameter | Value |
| :--- | :--- |
| **Consensus Mechanism** | AURA |
| **Finality Gadget** | GRANDPA |

## Time

Exact Runtime code specifying constants related to block time and production.

| Edgeware | Time | Slots\* |
| :--- | :--- | :--- |
| **Block** | 6 seconds | 1 |
| **Epoch** | 60 minutes | 600 |
| **Session** | 60 minutes \(600 Blocks\) | 600 |
| **Era** | 6 hours \(6 sessions\) | 3600 |

{% hint style="info" %}
This code is from [https://github.com/hicommonwealth/edgeware-node/blob/master/node/runtime/src/constants.rs](https://github.com/hicommonwealth/edgeware-node/blob/master/node/runtime/src/constants.rs)

It may be out of date on this page, refer to the link above for most up to date runtime data.
{% endhint %}

```text
    pub const MILLISECS_PER_BLOCK: Moment = 6000;
    pub const SECS_PER_BLOCK: Moment = MILLISECS_PER_BLOCK / 1000;

    pub const SLOT_DURATION: Moment = MILLISECS_PER_BLOCK;

    // 1 in 4 blocks (on average, not counting collisions) will be primary BABE blocks.
    pub const PRIMARY_PROBABILITY: (u64, u64) = (1, 4);

    pub const EPOCH_DURATION_IN_BLOCKS: BlockNumber = 1 * HOURS;
    pub const EPOCH_DURATION_IN_SLOTS: u64 = {
        const SLOT_FILL_RATE: f64 = MILLISECS_PER_BLOCK as f64 / SLOT_DURATION as f64;

        (EPOCH_DURATION_IN_BLOCKS as f64 * SLOT_FILL_RATE) as u64
    };

    // These time units are defined in number of blocks.
    pub const MINUTES: BlockNumber = 60 / (SECS_PER_BLOCK as BlockNumber);
    pub const HOURS: BlockNumber = MINUTES * 60;
    pub const DAYS: BlockNumber = HOURS * 24;
```

{% embed url="https://github.com/hicommonwealth/edgeware-node/blob/master/node/runtime/src/constants.rs" caption="" %}

## Staking

| **Parameter** | Value | Description |
| :--- | :--- | :--- |
| **Validator Slots** | 110 | The total number of slots for active validation. |
| **Validator Bonding Duration** | 28 hours | How long until you can unbond your funds after staking |
| **Slash Deferral Duration** | 28 Eras \(7 days\) | Prevents overslashing and validators "escaping" and getting their nominators slashed with no repercussions to themselves |
| **Slash Cancellation Vote** | Requires 3/4 of Council to Approve |  |
| **Validator Term Duration** |  | The time for which a validator is in the set after being elected. Note, this duration can be shortened in the case that a validator misbehaves. |
| **Nomination Period** |  | Countdown until a new validator set is elected according to Phragmen's method. |

## Democracy \(Referenda\)

| Parameter | Value | Description |
| :--- | :--- | :--- |
| **Launch Period** | 7 days | How long the public can select which proposal to hold a referendum on. i.e., Every week, the highest-weighted proposal will be selected to have a referendum |
| **Voting Period** | 7 days | How long the public can vote on a referendum. |
| **Enactment Delay** | 8 days | Time it takes for a successful referendum to be implemented on the network. |
| **Passing Vote Criteria** | Supermajority to pass |  |
| **Fast Track Voting Period** | 3 days | Minimum voting period allowed for an emergency referendum. |
| **Veto** | Not active |  |
| **Proposal Cancellation Vote** | 2/3 of council to Approve Cancellation |  |
| **Cool-off Period after Proposal Cancellation** | 7 days | The time a veto from the technical committee lasts before the proposal can be submitted again. |
| **Min. EDG Deposit to Vote** | 100 EDG |  |

**Vote Weighting by Lock Time**  
The schedule of weight boosts on a quadratic curve - meaning that exponentially increasing locktimes are required to achieve lesser proportional boosts in weight.

| Vote Weight | Locktime |
| :--- | :--- |
| 0.1x | None |
| 1x | 1x Enactment Period \(8 days\) |
| 2x | 2x Enactment Period \(16 days\) |
| 3x | 4x Enactment Period \(32 days\) |
| 4x | 8x Enactment Period \(64 days\) |
| 5x | 16x Enactment Period \(128 days\) |
| 6x | 32x Enactment Period \(256 days\) |

## Council Elections

| **Parameter** | Value | Description |
| :--- | :--- | :--- |
| **Term Duration** | 28 days | The length of a council member's term until the next election round. A new councilperson is elected every 28 days based on the Phragmen algorithm. If the term duration is changed the current term is affected when `BlockNumber % TermDuration ==0`, upon which a new council \(or councilperson?\) will be selected. |
| **Candidacy Bond** | 1000 EDG | The amount a user must bond to submit their candidacy. |
| **Voting Bond** | 10 EDG | The amount of EDG that a voter must lock to vote for Council. |
| **Council Member Slots** | 13 members | The size of the council. |
| **Runners-up Slots** | 7 members | The number of slots that will be displayed as a runner-up. |
| **Council Voting Period** | ?? | The council's voting period for motions. |

\*\*\*\*

## **Treasury**

| **Parameter** | Value | Description |
| :--- | :--- | :--- |
| **Budgeting Period** | 7 days | When the treasury can spend again after spending previously. |
| **Proposal Bond** | 5% and minumum 1000 EDG | The amount required to bond in order to propose a treasury spend. If approved, it is returned, if the proposal fails, it is burnt. |
| **Burn unspent treasury funds** | Off | This deactivates a burn of all  unspent treasury funds at the end of a budgeting period. |

\*\*\*\*

## **Signaling**

| Parameter | Value | Description |
| :--- | :--- | :--- |
| **Signaling Period** | 7 days | The length of time a signal proposal is active for engagement. |
| **Signaling Proposal Bond** | 100 EDG | The amount of EDG required to bond to submit a signaling proposal. |

## Identity

| Parameter | Value | Description |
| :--- | :--- | :--- |
| **Required Bond Per Identity** | 10 EDG | Bond required to store IDs on-chain. |
| **Required Bond Per Each Additional Identity Field** | 2.5 EDG | Bond required to store **additional** IDs on-chain **Beyond Legal Name.** |
| **Sub-Account Deposit** | 2 EDG | Amount required to deposit in order to create a sub account. |
| **Maximum Sub-Accounts** | 100 | The maximum number of sub account an account may have. |

## Economics

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
      <td style="text-align:left">.025</td>
      <td style="text-align:left">The min. inflation rate the system will permit.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Maximum Inflation</b>
      </td>
      <td style="text-align:left">
        <p>&lt;b&gt;&lt;/b&gt;</p>
        <p>0.1</p>
      </td>
      <td style="text-align:left">The max. inflation rate the system will permit.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Ideal Staking Rate</b>
      </td>
      <td style="text-align:left">0.8</td>
      <td style="text-align:left">The ideal proportion of EDG tokens staked compared to total EDG supply.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Falloff (Decay) Rate</b>
      </td>
      <td style="text-align:left">
        <p>&lt;b&gt;&lt;/b&gt;</p>
        <p>0.05</p>
      </td>
      <td style="text-align:left">The decay rate on inflation when the actual staking rate becomes greater
        than the ideal staking rate.</td>
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
      <td style="text-align:left">0.005</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Ideal Interest Rate</b>
      </td>
      <td style="text-align:left">12.5%</td>
      <td style="text-align:left">The ideal returns that an individual validator earns.</td>
    </tr>
  </tbody>
</table>

## Contract configuration

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

