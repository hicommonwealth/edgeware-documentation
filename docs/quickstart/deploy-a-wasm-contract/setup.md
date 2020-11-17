Setup
===

To follow this tutorial, you will need to set up some stuff on your computer.

## Substrate Prerequisites

To get started, you need to make sure your computer is set up to build Substrate.

If you are using __OSX__ or most popular __Linux__ distros, you can do it by running:

```bash
curl https://sh.rustup.rs -sSf | sh -s -- -y
```

```
rustup target add wasm32-unknown-unknown --toolchain stable
rustup component add rust-src --toolchain nightly
rustup toolchain install nightly-2020-06-01
rustup target add wasm32-unknown-unknown --toolchain nightly-2020-06-01
```

The final tool we will be installing is the ink! command line utility which will make setting up Substrate smart contract projects easier.

You can install the utility using Cargo with:

```bash
cargo install --git https://github.com/hicommonwealth/cargo-contract cargo-contract --force
```

You can then use `cargo contract --help` to start exploring the commands made available to you.
> **Note:** The ink! CLI is under heavy development and some of its commands are not implemented, yet!
