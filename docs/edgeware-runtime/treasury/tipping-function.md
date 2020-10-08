# Tipping Function

{% hint style="info" %}
Substrate Documentation for this function is at: [https://substrate.dev/rustdocs/master/pallet\_treasury/index.html\#tipping](https://substrate.dev/rustdocs/master/pallet_treasury/index.html#tipping)
{% endhint %}

The treasury module also contains a more ad-hoc way of distributing funds from the treasury to a single recipient, called Tipping.

1. Users join a tipping round.
2. Each user names an amount of EDG that a beneficiary may deserve, subjectively.
3. Once 50% of these users submits their amount, a countdown begins for the remaining undecided.
4. Once the countdown ends, the tipping round closes. 
5. The Treasury calculates the median of the tip submissions.
6. The beneficiary receives that median amount of EDG from the Treasury.

| Function Supported by UI at: |
| :--- |
| [Polkadot Apps](https://polkadot.js.org/apps/#/explorer) |

