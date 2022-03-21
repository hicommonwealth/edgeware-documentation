# Lockdrop Allocation Formula

## Concluding Parameters

From the [**Lockdrop Conclusion Metrics page**](https://commonwealth.im/edgeware/stats)**, backed up here:**

{% hint style="success" %}
The final ETH/EDG ratio is **1 ETH : 1,156 EDG.**
{% endhint %}

| Parameter | Value |
| :--- | :--- |
| Total Locked ETH | 1,199,728 ETH |
| Total Signalled ETH | 4,346,544 ETH |
| EDG Distributed to Lockers | 64.1% |
| EDG Distributed to Signals | 25.9% |
| EDG Distributed via Genesis | 10% |
| Effective Lockers ETH | 2772238 ETH |
| Number of ETH Addresses participating in Locks | 2869 |
| Number of ETH Addresses Participating in Signals | 1922 |
| Effective Signalers ETH | 1120407 ETH |
| Network Launch Date | Feb 17 2020 |
| ETH in Generalized Locks | 313,872 ETH |
| Additional effective ETH attributable to generalized lock | 251,098 ETH |

{% hint style="info" %}
Effective ETH is contributed ETH modified by the bonus, lock weight and EDG/ETH ratio.
{% endhint %}

## Lock-Allocation Calculation

In the lockdrop event, the number of EDG actually obtained by each locking user is determined by a formula:

$$
timingBonusModifer * lockWeight * userETHLocked*(totalEDG/totalETH)
$$

### Variables

**Timing Bonus Ratio:** User-Controlled Parameter.  
The earlier you lock in the event schedule's 7 bonus periods, the higher this bonus modifier is. Per the above schedule, the parameter options are:

| Time Period | Bonus Modifer |
| :--- | :--- |
| June 1 - June 15 | 1.5 |
| June 16- June 30 | 1.35 |
| July 1 - July 15 | 1.23 |
| July 16 - July 30 | 1.14 |
| July 31 - August 14 | 1.08 |
| August 15- August 29 | 1.05 |
| August 30 - August 31 | 1 |

**Weight:** User-Controlled Parameter.  
Participating via a three-month lock will get 1\(weight\) when distributing EDG tokens; Participating via a twelve-month lock will get 2.2 \(weight\) when distributing EDG tokens.

**User's Locked ETH:** User-Controlled Parameter  
The specific number of ETH the user locks.

**Total Allocatable EDG**: System Parameter  
\_\*\*\_Total EDG in at Edgeware genesis is 5 billion, or 5,000,000,000. 4.5 billion is distributed via the lockdrop event. Therefore, total allocatable EDG is 4,500,000,000.

**Total Locked ETH:** Aggregated User Contribution  
The total number of ETH locked.

**Ratio of EDG to ETH**:  
The number of lockdropped EDGs that one ETH can obtain. This parameter cannot be known until the end of the lockdrop event because the total ETH locked must be known. Since[ the event closed and stats have been published](https://commonwealth.im/edgeware/stats), it is understood to be **1 ETH : 1,156 EDG.**

