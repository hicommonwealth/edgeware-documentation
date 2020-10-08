# Economics

### Token Economics Information

| Value | Info |
| :---: | ---: |
| **Total Initial Supply** | 5 Billion |
| **Total Planned Inflation** | The total amount of EDG minted will remain the same year after year, causing the percentage inflation to be **disinflationary**, with yearly inflation falling to approximately 16.6% in the second year and so on. |
| **Maximum Token Supply** | Variable by governance action. |
| **Inflation Rate** | [Dependent upon the staking rate](https://docs.google.com/spreadsheets/d/1QCs1KgGGAEIDugOHHD6n8kI4UG2v5nO_DwXt-D8El4A/edit#gid=494484132) in the network, but maxes out at 20% as the staking ratio approaches 80% currently. This latter will likely shift to 50% through governance \(the 'ideal staking rate'\) |
| **Maximum Stake** | No maximum |
| **Minimum Stake** | No minimum |
| **Unbonding / Undelegating period** | 6 Hours currently \(unverified\) , but should become several days after an upcoming upgrade. |
| **Token Type** | Native Platform Token \(like ETH\) |
| **Ticker** | EDG |
| **Decimal Places** | 18 |
| **Inflation per Block** | ~95 EDG |
| **Ideal Inflation Rat**e | 158 EDG per block |

### Consensus

Edgeware uses Nominated Proof of Stake \(NPoS\) as its consensus method. There is a [known and limited](https://polkadot.js.org/apps/#/staking) number of validators in the active set and this active set number is decided by governance. Inclusion in the active set is determined by your total self-bonded and delegated stake. The minimum stake to get in the active set varies daily and depends upon the number of validators attempting to be included and the amount of stake on each. In a NPoS system, each elected validator has equal say in consensus and is rewarded equally, not according to the proportion of stake, as a result it is incentivized for a validator to distribute their stake and run multiple validator nodes-- not only among their own nodes but potentially among other validators to normalize stake across the set, something NPoS does to help prevent centralized stake.

{% hint style="info" %}
No names have been assigned for fractions of an EDG, we refer to them by the default dollars/cents \(1 EDG is a dollar, one EDG cent is 0.01 EDG.\) This is a good opportunity for a proposal.
{% endhint %}

### [Staking Estimator](https://docs.google.com/spreadsheets/d/1VlzTUDESbbfOggMRz3GyE9-VqR9MlOhNuoekBboKvLw/edit?usp=sharing) Spreadsheet

## Inflation

**Inflation is currently ~95 EDG / block.**

The genesis specification parameters \(in decimal\) related to this ideal condition, and what the algorithm uses are:

| Parameter | Value |
| :--- | :--- |
| Minimum Inflation | 0.025 |
| Maximum Inflation | 0.125 |
| Ideal Staking Rate | 0.800 |
| Decay Rate \(aka Falloff\) | 0.050 |

### Token Uses

On Edgeware, EDG has multiple functions.

* Staking 
* Voting \(Governance, elections, proposal making.\)
* Staking Delegation
* Voting Delegation
* Pay transaction fees for state changes in smart contracts.

### Token Supply Chart

### [See and edit the full sheet.](https://docs.google.com/spreadsheets/d/1bKuD0GnQr-HZIrPdos6UuVBfOu27MxAuKqF5t2llOHM/edit)

{% embed url="https://docs.google.com/spreadsheets/d/1bKuD0GnQr-HZIrPdos6UuVBfOu27MxAuKqF5t2llOHM/edit?usp=sharing" caption="" %}

