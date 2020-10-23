# FAQs

## FAQs

**How do I retrieve my ETH after the Lockdrop is over?**

[Use the Unlock tool at Commonwealth.im](https://commonwealth.im/#!/unlock)

[Read the full instructions at blog.edgewa.re](https://blog.edgewa.re/luc-101-retrieving-your-eth-from-the-lockdrop-contract/)

To get your ETH back from a Lockdrop User Contract, once your lock duration has ended, send a zero-value or greater transaction from any account to the contract address of the LUC.

The LUC will then return the ETH to the original address that sent this ETH to the Master Lockdrop Contract at the start of the Lockdrop Event. [Read a longer, detailed explanation at Blog.edgewa.re](https://blog.edgewa.re/luc-101-retrieving-your-eth-from-the-lockdrop-contract/)

**How can I access the EDG I got allocated to by lockdrop \(including signaling\)?**

At the time of participating in lockdrop, you must have generated a mnemonic seed phrase. Kindly import it on Polkadot UI \(optionally through Enzyme extension or polkadot\(.js\) extension\) or on the unofficially maintained android version of the Math wallet and you will get access to your EDG! Read more about account interactions here: [https://docs.edgewa.re/understanding-edgeware/accounts](https://docs.edgewa.re/understanding-edgeware/accounts)

**How many EDG will be minted in the genesis lockdrop event?**

The genesis of the Edgeware network will mint 5 Billion EDG tokens.

Of this 5 Billion, 90%, or 4.5 billion will be distributed through the lockdrop process. The 10% remainder is distributed to:

4.5% to Commonwealth Labs, the developers of Edgeware, and will not be used to fund development. 3% to Parity Tech for support services on their Substrate product. 2.5% reserved for Community Incentives, OSS development, or other network success goals.

For the 90% distributed in the Lockdrop Event, lockdrop participants obtain 'shares' or the ability to obtain EDG at a certain proportion to their locked or signaled ETH. The following chart shows these share weights:

| Duration of Lock | Method | Weighting | EDG Received |
| :--- | :--- | :--- | :--- |
| 0 months | Signal | 0.20x | 25% at launch, 75% 265 days later |
| 3 months | Lock | 1.00x | Upon Network Launch |
| 6 months | Lock | 1.30x | Upon Network Launch |
| 12 months | Lock | 2.20x | Upon Network Launch |

Ones final shares are a proportion of the 90%, not a determinate value until the lockdrop closes and the total amount of locked ETH are known. One can earn greater share weights through locking for longer durations or locking earlier.

**Lockdrop Early Participation Bonus: Schedule**

| Date Range \(2019\) | Bonus | Eth Cap |
| :--- | :--- | :--- |
| June 1 - June 15 | S50% | No Cap |
| June 16 - June 30 | 35% | No Cap |
| July 1 - July 15 | 23% | No Cap |
| July 16 - July 30 | 14% | No Cap |
| July 31 - August 14 | 8% | No Cap |
| August 15 - August 29 | 5% | No Cap |
| August 30 - August 31 | 0% | No Cap, end of lockdrop |

For [https://stats.edgewa.re](https://stats.edgewa.re) , we are planning to include a calculator with an estimation tool.

**How can I view participation statistics and results from the lockdrop?**

At Commonwealth.im: [https://commonwealth.im/\#!/stats/edgeware](https://commonwealth.im/#!/stats/edgeware)

**I am signaling participant. When my EDG will become transferable?**

25% EDG of signaling participants are already unlocked \(transferable\) and rest 75% EDG of are vested until 17th Feb 2021 \(1 year from mainnet launch\).

**Why infinite supply / no max cap on supply/ inflation needed?**

Inflation is necessary to reward those who secure the network \(validators and nominators\) and it is also utilized for ecosystem growth by means of the treasury. Currently, inflation is set to 95 EDG per block. No can have direct access to those EDG. Approx 20% gets distributed as staking rewards and the rest goes to the treasury.

**Why On-chain Treasury?**

It’s an on-chain fund which no one has direct access to! Edgeware has taken an incubator stance and seeking to support innovative projects/ideas utilizing the Edgeware network as a deployment platform. On-chain treasury provides funding\(s\) to such projects, onchain contractors and many innovative concepts on getting approval from the EDG holders directly or indirectly\(by means of onchain council\).

**Why can't I see my balance after network upgrade?**

Due to the network upgrade, some accounts need migration. Anyone can migrate anyone's account. More detailed information here: [https://commonwealth.im/edgeware/proposal/discussion/625-edgeware-postupgrade-account-migration](https://commonwealth.im/edgeware/proposal/discussion/625-edgeware-postupgrade-account-migration)

## TechnicalFAQs

**What is the difference between a node and a runtime upgrade? How do they interact?**

Node upgrade is an update to the client software. These changes are mostly about networking software and/or optimizations to the system that processes the runtime binary.

While runtime upgrade is a change in the underlying WebAssembly binary being run by the node/client software. These are changes to the blockchain’s state transition function.

