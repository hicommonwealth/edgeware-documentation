# Frequently Used Commands

## Running a node

To start up the Edgeware node and connect to testnet 0.9.0, run:

```text
./target/release/edgeware --chain=chains/testnet-0.9.0.json --name <INSERT_NAME>
```

To run a chain locally for development purposes:

```text
./target/release/edgeware --chain=local --alice --validator
```

To allow apps in your browser to connect, as well as anyone else on your local network, add the `--rpc-cors=all` flag.

To force your local to create new blocks, even if offline, add the `--force-authoring` flag.

## Generating keypairs

To create a keypair, install subkey with `cargo install --force --git https://github.com/paritytech/substrate subkey`. Then run the following:

```text
subkey generate
```

To create an ED25519 keypair, run the following:

```text
subkey -e generate
```

To create derived keypairs, use the mnemonic generated from a method above and run \(use `-e` for ED25519\):

```text
subkey inspect "<mnemonic>"//<derive_path>
```

For example:

```text
subkey inspect "west paper guide park design weekend radar chaos space giggle execute canoe"//edgewarerocks
```

## Public nodes

Commonwealth Labs maintains several public nodes for testnet v0.8:

* testnet1.edgewa.re
* testnet2.edgewa.re
* testnet3.edgewa.re
* testnet4.edgewa.re
* testnet5.edgewa.re
* testnet6.edgewa.re

**Syntax:**

* wss://testnet1.edgewa.re

  or \(if wss: fails\)

* ws://testnet1.edgewa.re:9944

