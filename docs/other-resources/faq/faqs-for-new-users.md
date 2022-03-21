# New Users

## General FAQ

### Is there an Ambassador Program?

Edgeware has a set of Working Groups open to anyone who wants to participate - doocracy!

[https://commonwealth.im/edgeware/proposal/discussion/373-introducing-edgeware-working-groups](https://commonwealth.im/edgeware/proposal/discussion/373-introducing-edgeware-working-groups)

### How can I view participation statistics and results from the lockdrop?

At Commonwealth.im: [https://commonwealth.im/\#!/stats/edgeware](https://commonwealth.im/#!/stats/edgeware)

### How do DOTs interact with EDG?

Initially, Edgeware is being launched as an independent chain \("solochain"\). This means that EDG will be used as the bonding and reward token for validators.

When Polkadot launches, Edgeware will be eligible to become a parachain. DOTs are used to provide shared security and for inter-parachain communication in the Polkadot Network, so if and when Edgeware becomes a Polkadot parachain, for the duration of that parachain status, it will not have validators for the state of finality of its own , but rather that validation will happen through the Polkadot relaychain's validator pool. However, EDG will still be used for gas fees, spam prevention, and bonding for on-chain activities \(e.g. governance\).

In the future, the network may vote to make Edgeware a relay chain, just like Polkadot. In this case, EDG may be used to provide security for child parachains.

### Are there video guides?

Here is a list of links for community videos and translated guides:

{% embed url="https://blog.edgewa.re/other-videos-guides-and-resources-multi-language-for-the-lockdrop/" caption="" %}

### What will Commonwealth Lab's relation to Edgeware be after launch?

We will remain a core developer interested in the health and success of the network, but once Edgeware launches, Commonwealth Labs will participate in governance just like any other as a minority token holder. We're building a governance UI, anonymous voting modules, and other governance tech that we will deploy on Edgeware and other networks. We hope that our improvements are voted in by EDG holders and implemented on Edgeware!

### What are the staking and token economics of the network?

There are initially 5,000,000,000 \(five billion\) EDG tokens minted, divisible up to 18 decimal places. Initially, inflation is set to 158 EDG per block. This implies approximately 997,220,160 EDG in the first year, or just under 20% inflation. The total amount of EDG minted will remain the same year after year, causing the percentage inflation to be disinflationary, with yearly inflation falling to approximately 16.6% in the second year. Additionally, a system-wide vote may further increase or decrease inflation. Half of the inflation will be voted upon by token holders for various uses.

### How many validators will there be?

Edgeware is intended to have a very large validation community, ideally several thousand when the network is mature. Additionally, any individual can delegate \(hence, DPoS\) to a Validator.

### Why should I validate?

Validators help provide security on Edgeware, since it's a PoS-based chain. Validators also earn fees from both the block reward and transactions. Earned tokens can be used to influence further governance decisions on the network. Validation is technical, and can be challenging. It may also be easier to delegate to a validator instead.

### How does Edgeware utilize Parity Substrate?

Parity Substate allows Edgeware developers to focus on improving the chain rather than developing infrastructure. Chains launched on Substrate generally do not have to deal with network or runtime level engineering changes. They can be natively extended with modules, which are written in Rust, compiled to Wasm, and linked into the client runtime. Modules can be voted into a chain by on-chain governance, at which point all clients will automatically download and run them, in a safe sandboxed environment. This makes the process of upgrading a chain much simpler and more accessible to a wide variety of developers!

### What happens if Edgeware is no longer a parachain once Polkadot Network exists?

Even if Edgeware is voted off the Polkadot parachain set or our lease otherwise expires, it will still work as a "solochain", where it's responsible for its own security. In that case, EDG validators will have to reboot the chain with the chain state at the time Edgeware exited the Polkadot relay chain.

### What will incentivize the dApp developers onto Edgeware over other networks?

There are numerous reasons to build on Edgeware. The first is that Substrate and the eventual Polkadot parachain status makes interoperability easy. Another is that the infrastructure is built with a light client-first mentality. This will enable future mobile portability to be seamless.

### How does Edgeware benefit the Ethereum ecosystem?

We are Ethereum supporters! We also believe Ethereum will benefit from the growth of complementary ecosystems.

1. Lockdrop: The lockdrop will timelock ETH for up to a year as people go "long ETH and EDG". Remember, only ETH holders can participate! This adds another layer of utility to ETH and lowers circulating supply, which will likely enhance the economic security of Ethereum as it switches to a Casper-style consensus.
2. Bridging Networks: We think one of the first proposals that the community should work on is a game-theoretically sound ETH-EDG bridge. In the long term, this will allows fees and value to both to ETH and EDG. With a bridge in place, we anticipate that Ethereum dapps/protocols will be able to use Edgeware to scale, much in the same way that Loom Network and other protocols help scale Ethereum. Similarly, any tokens created on Edgeware can be custodied and "moved" over to Ethereum via the bridge, where they can be used in Ethereum's DeFi network \(e.g. traded on 0x, collateralized on Maker and Compound, and bundled using Set\).
3. Accelerating Development: Edgeware is be a progressive network that will incorporate scaling and governance tech at a faster pace than Ethereum, but we expect most of these improvements will be backported to Ethereum. We think the net effect will be substantially beneficial for both ecosystems. As one example, at Commonwealth we are building a multi-chain governance tool to make governance on ETH, EDG, or any other chain easier, and Edgeware will allow us to test out several governance models that we will apply across the ecosystem.

### Is Edgeware a fork of Ethereum?

No, it's a new chain built on a completely different codebase \(Parity Substrate\) with a different runtime and security model. While Ethereum holders can participate in the lockdrop, EDG will otherwise be an entirely separate network. However, we anticipate that a bridge will be built for ETH-EDG so that both chains can work together.

### I don't see proof of my rewards from nominating.

Substrate is a little weird- there won't be a transaction or event that will show you where your balance increases from staking rewards. Using a Block Explorer that shows you your full balance like [https://edgeware.Subscan.io](https://edgeware.Subscan.io), enter your reward-destination \(stash or otherwise\) account address and monitor the balance over a day to check that it is increasing.

### How do I claim my EDG from the lockdrop?

No claim is necessary. When you participated in the lockdrop, you created an EDG Address. Your EDG is already at that address. You can check your balance with a Block Explorer. You may also need to convert your lockdrop address into the new format for a block explorer to find your account.

### Why is my withdrawal from an exchange taking a long time?

Edgeware launched with an early version of Substrate that experiences a lag in block finality. Most exchanges wait until blocks are finalized to process withdrawals. Most users see these complete within a few hours. This will be remedied in the Summer 2020 Upgrade to Substrate 2.

## FAQs for New Users

### Accounts & Balances

#### Where can I store EDG?

For storing \[and optionally staking\], you can use the recommended full-fledged wallet interface [Polkadot Apps](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fmainnet1.edgewa.re#/) \[along with optional [polkadot{.js} extension](https://polkadot.js.org/extension/)\]. [Watch a walkthrough🎥👆](https://youtu.be/IjoHHofQXcY)

[Clover extension wallet](https://chrome.google.com/webstore/detail/clover-wallet/nhnkbkgjikgcigadomkphalanndcapjk)\(beta\) can also be used as an alternative to the Polkadot JS extension.

If you are looking for mobile wallets, [Polkawallet](https://polkawallet.io/) and [Math wallet](https://mathwallet.xyz) are the options that support EDG and certain web3 functionalities on Edgeware network.

Also, Ledger support is currently being developed by Zondax.

#### I can't find my account using my public address in a block explorer.

Most block explorers require the version of the Edgeware Public Address that encodes the Edgeware Network ID - if you created your key/address in the Lockdrop or via the Polkadot UI or extension, you first need to regenerate your address using a program called Subkey before you can use it to search. Yu can always use your seed to connect to wallet services, regardless of the network ID.

#### I'm seeing two different addresses depending on what service I use.

Edgeware accounts may have two address forms - one that encodes a Substrate Default Network ID and one that encodes the Edgeware network ID. Using block explorers, you should use the Edgeware form, and for all other cases we recommend the Edgeware network ID form, regenerate yours by following these instructions:

### EDG Token

#### Where can I buy or acquire EDG? Is it listed?

At this time, there are several low liquidity markets \(~150$ daily volume\) that list EDG. You should examine the security of these exchanges before making any purchases. Never buy seed phrases directly, your funds can be stolen.

### Staking, Validation and Nomination

#### Can I start staking EDG?

Yes, Edgeware launched with a fully functional proof-of-stake nomination \(also known as delegation,\) and validation system. Any user that holds EDG can participate in securing the network and receiving benefits \(but also endure the risks of being slashed for a validators nonconformance.\)

#### How long does it take a waiting validator to become active? Why don't my nominators get selected?

Validators are elected from a pool of the top 60 most-bonded validators. This election method is not based on amount alone, but a complex algorithm called the Phragmen Method.

#### **When can I unbond my nominated tokens?**

Bonding periods last 7 days. After 7 days you need to click on the lock icon or use the withdrawUnbonded\(num\_slashing\_spans\) staking function \[in Extrinsic submission option under Developer’s tab \] which will prompt you to sign a transaction to make those EDGs transferable.

#### Why can't I send/sign my Nomination transaction?

* Check that the Controller account has funds to pay transaction fees, this is the most common reason for issues. **If you get this error**: `staking.nominate`

  `submitAndWatchExtrinsic(extrinsic: Extrinsic): ExtrinsicStatus:: 1010: Invalid Transaction: Payment`

* Check that your Destination field in the Polkadot UI is set to the network default - and not to Kusama or other networks.

#### Why is it recommended to use a different account for Stash and Controller?

Separation of roles helps understand what accounts are performing what transactions, and allows us to disconnect the stash for security - making our wallets 'colder.' while still authorizing a controller to perform certain actions. You dont have to do this, but it is recommended.

#### How often do I receive a reward from Staking?

Every 'era,' which is roughly 6 hours. An era is a category of block time. [See more about time.](https://docs.edgewa.re/understanding-edgeware/network-parameters)

#### How do I see my bonded versus frozen versus free balances in my accounts?

You can use the Polkadot UI, then click Chain State tab to query your account for various parameters.

### Polkadot UI

#### How do I connect to Edgeware Mainnet? OR I tried but it won't connect.

Click the network logo in the top right, and select Edgeware mainnet from the drop down. If you experience connection issues, try changing the endpoint using the custom endpoint option. See the following for other network endpoints:

### Governance

#### One-person-one vote - what will prevent malicious players from signing on multiple nodes if it will cost little?

We provide a variety of tallying rules for certain governance features on Edgeware. The core governance is run with coin-weighted voting, with extensions that mimic a form of quadratic voting based on locking time \(I.e you get more weight by locking longer\). Therefore what you ask is not wholly correct. Some tally types are inherently and unavoidably vulnerable to certain tactics- if someone wants to run a signaling poll with one person one vote that’s their decision, but we can provide guidance about results and process.

### Miscellaneous

#### How Edgeware is different is that ‘x’ project?

Every project is unique in its own perspective. You may find some similarities in Edgeware and the ‘x' project. Though we should consider different projects as one of the essential parts of the ecosystem rather than non-healthy competitors. Also, it wouldn't be a good idea to talk on ‘x' project’s behalf. As Edgeware and the ‘x' project offer different prospects to the Crypto Ecosystem by different means which you can't directly compare. There will be many blockchains with complex native smart contract support like Edgeware has. But Edgeware aims to be an ecosystem and one-stop solution platform for various types of deployments. Native EVM support, interoperability with the current DeFi ecosystem on Ethereum through edgeth bridges, incubator stance, initiatives through different working groups are the major proposed things which make Edgeware different. \(Being a potential parachain also opens up possibilities not only for the polkadot relay chain but also for other parachains to utilize the bridges built by Edgeware.\)

We would recommend going through the following resources to know more about Edgeware:

• [Roadmap](https://blog.edgewa.re/edgeware-2020/)

• [Edgeware Docs](https://docs.edgewa.re/)

#### Can I trade EDG on decentralised protocols like Uniswap or any DEXs?

Currently, you can't trade EDG on any swap protocols/portals like Uniswap. EDG is a native token of Edgeware blockchain, not an erc20 token. But there are plans for Uniswap integration through Tokyo Network Upgrade \(Bridging to Ethereum\) and it is scheduled for Fall of 2020. Edgeware aims to build Ethereum Bridges to setup interoperability of EDG into the existing ETH DeFi ecosystem, allowing for the creation of EDG / ETH, wEDG / DAI, and other pairs on Uniswap and Balancer.

#### Recently I participated in democracy voting. How can I make those locked EDGs transferable after the locking period gets over?

Go to the Extrinsics option under Developer tab in Polkadot Apps and by selecting ‘democracy’ under the extrinsic type, submit extrinsic unlock\(target\).

