# WASM Ballot Contract

## Introduction

In this chapter, we will teach you how to use ink! to write more complex contracts.

We will build a "Ballot" contract which will allow users to add proposals to a ballot and vote on them. The users will be able to register themselves as a voter with a function call and there will be a chair person \(owner\) of the contract that will oversee the process.

Over the course of this chapter you will learn:

* To build custom structs
* To store custom structs in vectors and hash maps
* To safely get and update the structs in these collections
* To use ink\_prelude crate
* To use traits like Clone, Debug, PackedLayout and SpreadLayout

