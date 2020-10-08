---
description: >-
  Author: Thom Ivy on behalf of Commonwealth Labs-- Originally posted at
  Commonwealth.im and adapted for docs.edgewa.re.
---

# Gini Coefficient of Edgeware

## **Gini Coefficient Analysis**

The total ETH locked in the standard process finalized at 1,199,728 ETH, with signaled funds at 4,346,544 ETH. This demonstrates strong confidence and interest in both the contracts underlying the lockdrop, but also the advance in blockchain technology that Edgeware represents. Today there exist over 4000 different Edgeware addresses largely created in the lockdrop process, from over 10,000 transactions.

The lockdrop mechanism was primarily designed to distribute a utility token in a more decentralized and equal fashion while strongly selecting for committed users and holders, this was achieved by ‘supercharging’ the power of small amounts by allowing for the use of time as leverage: lock longer, get more.

For many cryptonetworks, the decentralization of the system is analyzed using [the gini coefficient](https://en.wikipedia.org/wiki/Gini_coefficient), which looks at the distribution of wealth. We provide the gini coefficient of 0.694 for Edgeware. The following charts show the distribution of Edgeware tokens, and then the [Lorenz curve](https://en.wikipedia.org/wiki/Lorenz_curve) and gini coefficient of our analysis.

![Distribution of Edgeware tokens of top 4.2% of Accounts](https://lh3.googleusercontent.com/TpeGRDY7Wi4xvMkw968PksrPn0ZuwxM6BSwwVXGguwg_LXFbruyjQIKnwybLbR4jOR2eOx5vDrkshBjQzmrg3-yWZWzIylmr1TpKd3uROcTiIna49yDkD-lWWPO81sa_ASNtOEoV)

![Lorenz Curve and Gini Coefficient of Edgeware Token Distribution](https://lh4.googleusercontent.com/fKYymIwRa5YX8gC5J27wuzIaqtGHltwdfaNqALCdi8R4d1yFgL4obXHFj3pWi4Wiqub3yItY_xnwMSNxzeIqmIAlScpgk34D8ufa_rMvQPY_ecrhSEOArmGjrioBhw-beFh-uSD2)

### Caveats

* Some of the largest distributions are from [exchanges like Binance](https://www.binance.com/en/blog/376024539711221760/Did-You-Hold-ETH-on-Binance-Congratulations-Youll-Get-Free-Edgeware-Tokens). These accounts signaled on behalf of their users, and have announced plans to distribute the allocations to the appropriate ETH holders - so their holdings don’t actually correspond to the individuals. This creates a bias towards a higher gini coefficient than the network actually possesses. 
* Multiple addresses may be mapped to the same holder - which could affect the final coefficient in either direction - it is impossible to tell which accounts may or may not be in the control of the same person. 
* Most importantly, Gini coefficient analysis is sensitive to small amounts, of which Edgeware’s distribution has a high number. 
* For our final analysis of the Edgeware distribution, we modeled the [Google BigQuery network analysis](https://cloud.google.com/blog/products/data-analytics/introducing-six-new-cryptocurrencies-in-bigquery-public-datasets-and-how-to-analyze-them) conditions, in order to create a more comparable set of results to existing networks. As Edgeware, being new, doesn’t have anywhere near 10000 addresses, we can find use a percentage as a relative measure.  [Coinmetrics.io reports that at the time of Google’s analysis,](https://coinmetrics.io/charts/#assets=btc,eth_left=AdrActCnt_right=AdrActCnt_zoom=1567468800000,1570060800000) active account numbers for Ethereum, for instance, had a total of 233.701k addresses. As Google looked at the top 10,000 addresses, they examined the top 4.2% of accounts.   
* For the sake of comparison then, the top 4.2 percent of Edgeware addresses form the basis of[ our dataset](https://docs.google.com/spreadsheets/d/1Dmf0ZK8WBRPBLZ95Gf95gHIEMB2uhTG5v9yjesgABI4/edit#gid=71362133). In order to find the gini coefficient, we entered the values of these accounts into a [simple gini calculator. ](http://shlegeris.com/gini)This provides the coefficient for roughly 90% of all lockdrop-distributed Edgeware tokens. Let’s compare Edgeware’s gini of 0.694 to top cryptonetworks as found by Google BigQuery:  

![](https://lh4.googleusercontent.com/aL5M2FDvbegv8LLXnvauhD6C7efMA4yKd33ur-Puld_NBb_Q6pJFqcTOz4SOXDP22R83j2xUCNGb50aKjaG7ZkKGlGWtaVhclIhdrAzlcroLXWw07sqQ_JJag3gIZfZdvtamjLoP)

_Gini Coefficients of Popular Cryptonetworks \(Top 10k Addresses\)_ [_measured by Google BigQuery_](https://cloud.google.com/blog/products/data-analytics/introducing-six-new-cryptocurrencies-in-bigquery-public-datasets-and-how-to-analyze-them)

If we focus on the initial launch times of these networks, no network with less than 0.55, **placing the Edgeware lockdrop distribution firmly as the most decentralized token distributions.** \(Google notes in their analysis that Dash’s numbers may be unreliable due to privacy features.\)

With the lockdrop contracts proven to both function and to be secure, we expect future uses of the mechanism to be even fairer as bonus structures are improved and users trust contracts to participate in longer locktimes.

### **Long Term Interest**

In ICOs or other methods to distribute tokens, capital begets capital. However, in a lockdrop, users can be increased through time preference--bonuses for participating longer. In this way, it allowed many small ETH amount holders to show their preference. The overwhelming proportion of lockers chose not to lock for 3 months, but the maximum amount of time, 12 months. This shows us that they have a long term interest in the network. Moreover, individuals signaled their participation in additional ways, with over 130 addresses indicating that they’d like to validate. This amount has been backed up by the more than ~70 validators participating over the course of this last testnet.

## **Continued Governance Experimentation**

**by Dillon Chen**

As we discussed before launching the lockdrop. One goal for us was to further experimentation around governance. It’s safe to say that a few seeds have been planted. First, we’ve seen many teams working on further experiments in token distribution--for example, NuCypher and the [Worklock](https://blog.nucypher.com/the-worklock/). By adding a convenant and allocating only to those who are validating _and_ adding slashing in things get much more interesting.

This experimentation wasn’t limited to other projects, the same lockdrop allocation was also used to spin up a separate network, Straightedge. We’re excited to see this develop.

On [Commonwealth](https://commonwealth.im/#!/edgeware/proposal/discussion/7), there have been community participants suggesting that we could make the lockdrop more than just a single asset. This is something that the Edgeware governance system could vote on post-launch for any future EDG distributions. Or a further experiment. Governance is an ongoing process, with that we’ve built tooling for EDG holders to easily participate in this process community to _fully_ utilize the token:

* Vote on council members to help shape the future direction of Edgeware.
* Delegate EDG to validators and bond for their own validator positions to help secure the Edgeware network.
* Vote on treasury proposals to help fuel ongoing experiments, propel adoption, and reward the network’s most active contributors.
* Climate DAOs
* [Funding the ambassador program](https://commonwealth.im/#!/edgeware/proposal/discussion/43)
* Hosting a worldwide **EdgeCon**

### **What does this lead us?**

There is quite a bit of uncharted territory for the community to explore. There are more than a few proposals that we’re happy to share on Commonwealth. In another few months, we’ll be sharing updates on the improvements the community has achieved!

[See Commonwealth.im for existing proposals.](http://commonwealth.im/)

