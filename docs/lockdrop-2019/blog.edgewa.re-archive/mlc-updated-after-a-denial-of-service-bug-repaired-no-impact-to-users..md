---
description: 'Published July 1 2019, written by Drew Stone. Archived from blog.edgewa.re'
---

# MLC Updated after a Denial of Service bug repaired, no impact to users.

## 

All existing Lockdrop participant funds are safe and unaffected. We have redeployed a new contract, updated the Lockdrop page, and the stats page to reference both contracts.

* 
_**No Lockdrop participants’ funds are affected by this issue**. We thank_ [_**Neil McLaren**_](https://medium.com/@nmcl/gridlock-a-lockdrop-bug-73b8310608a9) _for making us aware of this DoS bug in the main lockdrop contract._

[_See the pull request associated with this fix on Github._](https://github.com/hicommonwealth/edgeware-homepage/pull/9)

We have learned of an attack that can prevent _future_ lockers from interacting with the Master Lockdrop Contract **\(MLC Ver.1\)**.

In the process of creating a lock, the Master Lockdrop Contract performs several checks to ensure that locking operations are completed successfully and without risk to users. One of those checks ensures that newly created Lockdrop User Contracts have the expected balance.

By calculating the anticipated address of a future Lockdrop User Contract, an attacker can send funds to that address, and later, when the new Lockdrop User Contract is created at this address, the unexpectedly greater amount will cause this check to fail.

If this check fails, it prevents any further lockers from participating.

To emphasize, all existing Lockdrop participant funds are safe and unaffected. \(Lockdrop User Contracts only have one function call, with no assert checks, to send funds back to the original locker's address.\) We have redeployed a new contract, updated the Lockdrop page, and updated the stats page to reference both contracts.

### Technical Explanation <a id="technical-explanation"></a>

We will now describe in-depth: the system , the DoS bug, and our steps to resolve the issue and enable service in the event the bug is triggered.

To start, let us dive into how Lock User Contracts **\(LUC\)** are maintained/created. Every single time a user calls the `lock` function on the **MLC**, an **LUC** is created. Every LUC has the following structure:

```text
contract Lock {
    constructor (address owner, uint256 unlockTime) public payable {
        assembly {
            sstore(0x00, owner)
            sstore(0x01, unlockTime)
        }
    }
    
    function () external payable { // payable so solidity doesn't add unnecessary logic
        assembly {
            switch gt(timestamp, sload(0x01))
            case 0 { revert(0, 0) }
            case 1 {
                switch call(gas, sload(0x00), balance(address), 0, 0, 0, 0)
                case 0 { revert(0, 0) }
            }
        }
    }
}
```

This contract is created with an `owner` and an `unlockTime`. Whenever _any_ transaction is sent to an **LUC**, it asks:

1. Is the current time greater than the `unlockTime`?
2. If \#1 is true, send the **LUC**'s balance to the `owner`.

A **LUC** is created when a user calls the `lock` function on the **MLC**, outlined below:

```text
    function lock(Term term, bytes calldata edgewareAddr, bool isValidator)
        external
        payable
        didStart
        didNotEnd
    {
        uint256 eth = msg.value;
        address owner = msg.sender;
        uint256 unlockTime = unlockTimeForTerm(term);
        // Create ETH lock contract
        Lock lockAddr = (new Lock).value(eth)(owner, unlockTime);
        // ensure lock contract has all ETH, or fail
        assert(address(lockAddr).balance == msg.value);
        emit Locked(owner, eth, lockAddr, term, edgewareAddr, isValidator, now);
    }
```

The above shows that when a new **LUC** is created all the ETH sent to the `lock` function of the MLC is instantly **forwarded** to the **LUC**. In the line afterwards, it asserts that the entirety of the balance has arrived in the **LUC**. Therefore by design, the **MLC** never holds any ETH and only acts as a proxy on behalf of locking and signaling participants. This assertion unfortunately is too restrictive and has the denial of service bug we are discussing today. Namely:

`assert(address(lockAddr).balance == msg.value);`

This statement can fail indefinitely if a user sends ETH to the future **LUC** that is to be created next. If there exists ETH already at that balance then the total sum would be `msg.value + pre_sent_balance`, which would fail the above assertion and reject, ultimately preventing any future user from locking in this **MLC**.

Instead, to fix this, we can change this line to  
  
`assert(address(lockAddr).balance >= msg.value);`

to prevent any user from stopping locks from being created.

### Why is this possible? <a id="why-is-this-possible"></a>

Ethereum contract addresses are deterministic. The are generated as a function of the creator address and the nonce of the address in the contract creation transaction. Contracts, too, have nonces. These nonces however only increment when they create contracts.

Since the **MLC** creates individual **LUC**s when users call `lock`, it is possible to determine future **LUC** addresses. In this case, one can send a future **LUC** any non-zero amount of Ether to make this assertion fail.

This prevents new lock contracts from being created, which means the contract nonce cannot increment any further.

### Resolution <a id="resolution"></a>

We have addressed the bug above by ensuring that the assertion encodes a greater-than-or-equal-to relation and have redeployed a new [**MLC**](https://etherscan.io/address/0xfec6f679e32d45e22736ad09dfdf6e3368704e31).

While **MLC Ver.1** has already been deployed \(and will remain live\) at the following address:

`0x1b75B90e60070d37CfA9d87AFfD124bB345bf70a`

**MLC Ver.2** has been deployed to address:

`0xFEC6F679e32D45E22736aD09dFdF6E3368704e31`

While there is a new contract, **MLC Ver.2**, this does not in any way invalidate previous locks or previous signals. Locks on both contracts will be honored, and signals from either contract will be accepted for inclusion in the final snapshot and genesis allocation.

