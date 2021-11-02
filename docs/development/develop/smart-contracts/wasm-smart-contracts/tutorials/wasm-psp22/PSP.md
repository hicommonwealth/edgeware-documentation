# EIPs - Ethereum Improvement Proposals

As described in the ERC20 chapter, Ethereum got a bunch of standard for different token contracts. 
The most popular are:
* [ERC20 Token Standard](https://eips.ethereum.org/EIPS/eip-20)
* [ERC721 Non-Fungible Token Standard](https://eips.ethereum.org/EIPS/eip-721)
* [ERC1155 Multi Token Standard](https://eips.ethereum.org/EIPS/eip-1155)


These standards define the interface that the contracts should implement. It will ensure interoperability between contracts (as it guarantees the signature of functions calls are standardized) and implement the most simple yet pure business logic.
As Ethereum uses EVM, these standards perfectly fit its specificities.

Apart from these well-known ERC token standards, other Ethereum standards exist that specify a standard at various levels for different purposes (see the complete list: [Ethereum Improvement Proposals](https://eips.ethereum.org/)).

# PSPs - Polkadot Standards Proposals
Polkadot ecosystem needs its own set of standards to fit ecosystem needs. These standard are called [Polkadot Standards Proposals (PSPs)](https://github.com/w3f/PSPs).

## PSP22

The [PSP22 Fungible Token standard](https://github.com/w3f/PSPs/blob/master/PSPs/psp-22.md)  is inspired by the ERC20 from Ethereum. It targets every parachain that integrates pallet-contract to enable WASM smart contracts.
It is defined at ABI level, so it should be used for any language that compiles to WASM (and is not restricted to ink! specifically).

PSP22 will have a double impact:
* On Parachain level, it will ensure the PSP22 is used to enable true interoperability. 
* In the multi-chain future, it will secure interoperability of all token standards (PSP22 and the next coming) between differents parachains or other substrate base chains.

It also helps to have a predefined interface for specific token standards to ensure exhaustive logic is implemented. 
It will also encourage to share the most performant & secure implementation.

{% endtab %}
{% endtabs %}
