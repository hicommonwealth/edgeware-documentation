# Treasury

While validators are often the only stakeholder natively incentivized in other blockchains, Edgeware has a treasury mechanism to permit creative incentivization of all stakeholders in the ecosystem, including core and dapp development, ecosystem support and much more. These funds can be deployed through a Treasury Spend action which is subject to council approval. 

### Technical Process of a Treasury Spend

1. Treasury Spend Proposed
2. Council either adopts or refuses the proposal.
3. If approved, it enters a queue within a budget period of 24 days. 
   1. The treasury attempts to fulfill as many spends in the queue within this time period.
   2. At the end of a budget period, the remaining treasury balance is subject to a small percentage burn. This incentivizes the usage of funds and creates deflation through the destruction of EDG.
4. If refused, the treasury proposal remains able to be accepted until the end of the 24 day period, then it is removed from the consideration table but can be resubmitted.

### EDG Accrual to the Treasury

The treasury obtains funds in several ways that mimic governments - minting, fees and taxes.

1. **Minting:** A portion of the EDG produced with each block goes to the treasury.
2. **Slashing:** When a validator is slashed for any reason, the slashed amount is sent to the Treasury. Slashed EDG may also accrue to the treasury through failed governance proposals.
3. **Transaction fees**: A portion of each block's transaction fees goes to the Treasury, with the remainder going to the block author.
4. **Staking inefficiency:** [Inflation](https://wiki.polkadot.network/docs/en/learn-staking#inflation) is designed to be ~20% in the first year, and the ideal staking ratio is set at 80%, meaning 80% of all tokens should be locked in staking. Any deviation from this ratio will cause a proportional amount of the inflation to go to the Treasury. In other words, if 80% of all tokens are staked, then 100% of the inflation goes to the validators as reward. If the staking rate is greater than or less than 80%, then the validators will receive less, with the remainder going to the Treasury.
5. **Lost Deposits:** These may be abandoned bonds from voting, proposals or otherwise.

{% hint style="info" %}
**Parameter Note:** The _ideal staking ratio_ used in the Edgeware economic model is currently 80%.  _Inflation_ is currently set to about 20%, or 158 EDG per block.
{% endhint %}

**Next**, read about proposing a Treasury Spend action.

