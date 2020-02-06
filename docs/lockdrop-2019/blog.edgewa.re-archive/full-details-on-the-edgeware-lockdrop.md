---
description: 'From May 21 2020, by Thom Ivy and Drew Stone. Archived from blog.edgewa.re'
---

# Full Details on the Edgeware Lockdrop





![Full Details on the Edgeware Lockdrop](https://blog.edgewa.re/content/images/size/w2000/2019/05/EWLD-Illus1Artboard-1@3x-4.png)

_The_ [_mainnet Edgeware Lockdrop contract_](https://etherscan.io/dapp/0x1b75b90e60070d37cfa9d87affd124bb345bf70a) _is located on the Ethereum network at:_

`0xFEC6F679e32D45E22736aD09dFdF6E3368704e31`

_OLD MLC \(1.0\) **Do not use**:_ `0x1b75b90e60070d37cfa9d87affd124bb345bf70a`

_The Edgeware Lockdrop UI:_  
[https://edgewa.re/lockdrop](https://edgewa.re/lockdrop)

####  <a id="see-our-other-articles-on-the-lockdrop-process-"></a>

### **About Edgeware** <a id="about-edgeware"></a>

Edgeware is a new Proof of Stake blockchain protocol built on Substrate. It runs WebAssembly smart contracts and features on-chain governance for updating the core runtime logic. It has delegatable democratic and council-based forms of governance that can help fund new initiatives in the space and upgrade existing logic with new features and use cases.

Edgeware is being developed by Commonwealth Labs and is supported by the amazing work of the Parity team for their development of Substrate. The Edgeware launch will occur 3 months from the start of the Edgeware Lockdrop, where all lockdrop participants will be rewarded with nearly 90% of the initial genesis allocation of EDG tokens.

### **About Lockdrop Events** <a id="about-lockdrop-events"></a>

A lockdrop is a new, innovative funding mechanism that aligns token holders of potentially _many_ chains to seed growth for a new chain or project. Users time-lock some or all of their tokens of an approved kind, in a unique, user-specific smart contract for varying amounts of time _or_ signal their intent to participate in the project without locking any tokens, however these signaling users will receive a  smaller reward per token. Tokens that are locked within a lockdrop are returned to respective locker after the specified date. Therefore, all participants earn tokens on a new chain at a low-risk—that of the opportunity cost of locking—and are immediately able to participate in the decision-making of a new blockchain.

### **The Edgeware Master Lockdrop Contract \(Edgeware MLC\)** <a id="the-edgeware-master-lockdrop-contract-edgeware-mlc-"></a>

The Edgeware Lockdrop will run on the Ethereum blockchain at this address `0x1b75b90e60070d37cfa9d87affd124bb345bf70a`. The _'Master' Lockdrop Contract \(**Edgeware MLC,**_**\)** allows users to lock ETH as described above for 3, 6, or 12 months, or to signal ETH, which has no lock duration. Every lockdrop user receives a unique, independent Lock contract, tailored to and only redeemable by the creator's account- the _Edgeware Lockdrop User Contract_ _**LUC**_. To clarify, **no Ether is stored in the MLC** \(the smart contract that 'generates' all the Lockdropper's Contracts.\) Instead, all locked Ether are timelocked to the sender's **LUC** for their respective lock term.

Below you can find snippets of functions for the ULC as well as for the MLC, which have been [audited by Quantstamp](https://arena-attachments.s3.amazonaws.com/4282493/a155dc84aa1dfba4cfd3dc6be1e1ebdc.pdf?1557965252).

![](https://blog.edgewa.re/content/images/2019/05/EWLD-Illus1Artboard-1@3x-1.png)

**Lockdrop User Contract \(LUC\)**

A LUC is created for each individual lock. It stores an _owner_ and can return all locked ETH to that owner once the _unlock time_ has passed **and** a simple transaction is sent to this contract with enough gas \(between 21000-30000\).

In the next two sections, we'll discuss the technical features of lock and signal.

**Lockdrop.lock**

The lockdrop _lock function_ creates a new LUC for the sender and emits an Event indicating the following information:

1. The amount of ETH they want to lock within an individual LUC
2. The Edgware public address that they want the EDG awarded from this timelocked ETH to be allocated to
3. Whether they are interested in validating on the Edgeware network

```text
contract Lock {
    constructor (address owner, uint256 unlockTime) public payable {
        assembly {
            sstore(0x00, owner)
            sstore(0x01, unlockTime)
        }
    }
    
    /**
     * @dev        Withdraw function once timestamp has passed unlock time
     */
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

LUC Constructor in the MLC

```text
/**
* @dev        Locks up the value sent to contract in a new Lock term
* @param      The length of the lock up
* @param      edgewareAddr: The bytes representation of the target edgeware key
* @param      isValidator:  Indicates if sender wishes to be a validator
*/
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

Lock Program of the LUC

#### NOTE: SIMPLY INDICATING YOUR INTENT TO BE A VALIDATOR DOES NOT GUARANTEE YOU WILL BE SELECTED TO BECOME A VALIDATOR. VALIDATORS WILL BE SELECTED FROM THE LARGEST LOCKS FOR EACH PARTICULAR EDGEWARE PUBLIC ADDRESS. <a id="note-simply-indicating-your-intent-to-be-a-validator-does-not-guarantee-you-will-be-selected-to-become-a-validator-validators-will-be-selected-from-the-largest-locks-for-each-particular-edgeware-public-address-"></a>

**Lockdrop.signal**

The lockdrop signal function allows any account—both externally owned accounts and contract accounts—to signal their balance towards the lockdrop. These participants will specify the intended Edgeware public address where their genesis EDG tokens will be allocated to as well as information pertaining to the signaling account type.

1. For externally owned accounts \(EOAs\), one can submit their EOA public address as the `contractAddr`. When the `msg.sender` equals the contractAddr, it is assumed one is signaling from their EOA.
2. For contract accounts, one must submit the `contractAddr` and `nonce` that allowed `msg.sender` to create the contract at address `contractAddr`. This allows users to signal ETH that may be held by smart contracts towards the Edgeware lockdrop.

#### NOTE: YOU CAN ONLY SUCCESSFULLY SIGNAL FROM CONTRACTS IF YOU CONTROL THE PRIVATE KEYS FOR THE RESPECTIVE PUBLIC ADDRESSES THAT CREATED THESE CONTRACTS. <a id="note-you-can-only-successfully-signal-from-contracts-if-you-control-the-private-keys-for-the-respective-public-addresses-that-created-these-contracts-"></a>

\(This is due to the `didCreate` modifier.\)

```text
/**
* @dev        Signals a contract's (or address's) balance decided after 				lock period
* @param      contractAddr:  The contract address from which to signal the 				balance of
* @param      nonce:         The transaction nonce of the creator of the 				contract
* @param      edgewareAddr:   The bytes representation of the target 					edgeware key
*/
function signal(address contractAddr, uint32 nonce, bytes calldata edgewareAddr)
    external
    didStart
    didNotEnd
    didCreate(contractAddr, msg.sender, nonce)
{
    emit Signaled(contractAddr, edgewareAddr, now);
}
```

Signal Function

