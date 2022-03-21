# Frequently Used Commands

## Generate Keys with the newly added Edgeware Network ID

```text
subkey -n edgeware generate
```

## Running a node

To start up the Edgeware node and connect to testnet 3.0.5 \(This may be out of date!, run:

{% hint style="danger" %}
The testnet shown here may be out of date. Check the version and JSON name.
{% endhint %}

```text
./target/release/edgeware --chain=chains/testnet-3.0.5.json --name <INSERT_NAME>
```

To run a chain locally for development purposes:

```text
./target/release/edgeware --chain=local --alice --validator
```

To allow apps in your browser to connect, as well as anyone else on your local network, add the `--rpc-cors=all` flag.

To allow apps in your browser to connect, as well as anyone else on your local network, add the `--rpc-cors=all` flag.

To force your local to create new blocks, even if offline, add the `--force-authoring` flag.

## Generating keypairs

To create a keypair, install subkey with `cargo install --force --git https://github.com/paritytech/substrate subkey`.

Then run the following:

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

```text
subkey inspect "<mnemonic>"//<derive_path>
```

For example:

```text
subkey inspect "west paper guide park design weekend radar chaos space giggle execute canoe"//edgewarerocks
```

```text
subkey inspect "west paper guide park design weekend radar chaos space giggle execute canoe"//edgewarerocks
```

## Public nodes

Commonwealth Labs maintains several public node on mainnet and testnet. Please refer to the following page for the latest node contacts.

**Syntax:**

* wss://testnet1.edgewa.re

  or \(if wss: fails\)

* ws://testnet1.edgewa.re:9944

