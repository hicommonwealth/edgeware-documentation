---
description: >-
  This page draws from the Edgeware White Paper to provide an intro to Edgeware
  smart contracts.
---

# Smart Contracts on Edgeware

Edgeware smart contracts may be written in any Wasm-compatible higher level language. Already, there are well-tested toolchains for compiling C, C++, and Rust to Wasm, and independent work is in progress for compiling a subset of JavaScript to Wasm through the AssemblyScript project. 

{% hint style="info" %}
Any WASM-compatible higher level language can be used to write Edgeware Smart Contracts, including Rust, Ink! \(a subset of Rust by Parity Technologies\) and AssemblyScript. 
{% endhint %}

Edgeware will also benefit from improvements in security, portability, and expressiveness as Wasm toolchains are further developed by other blockchain and web infrastructure projects. Otherwise, contracts function much in the same way as they do on Ethereum or other EVM-compatible blockchains.

Any user with an EDG balance may deploy a contract, and contracts can call other contracts as well. Gas, denominated in EDG, must be bought upfront and limits computation. Message calls use gas up to the transaction limit, with any excess refunded. If all gas is used, computation terminates, and effects are reverted. Contracts will also be able to interact with other Edgeware modules through a limited set of whitelisted interfaces, in particular, to query accounts in the Identity and Council modules. 

Other improvements to the smart contract system, like parallelized transactions and state rent are expected to follow after the chain launches.

