# Install Edgeware



#### Quickstart

If your device is clean \(such as a fresh cloud VM\) you can use this script for an automated setup:

```text
./setup.sh
```

Otherwise, proceed with the full instructions below.

#### Manual setup

Install system dependencies:

Linux:

```text
sudo apt install cmake pkg-config libssl-dev git clang libclang-dev
```

Mac:

```text
brew install cmake pkg-config openssl git llvm
```

Install Edgeware dependencies:

```text
curl https://sh.rustup.rs -sSf | sh
rustup update stable
rustup update nightly
rustup target add wasm32-unknown-unknown --toolchain nightly
cargo install --git https://github.com/alexcrichton/wasm-gc
```

Build Edgeware:

```text
cargo build --release
```

Ensure you have a fresh start if updating from another version:

```text
./scripts/purge-chain.sh
```

To start up the Edgeware node and connect to testnet 0.9.9, run:

```text
./target/release/edgeware --chain=edg-0.9.9 --name <INSERT_NAME>
```

