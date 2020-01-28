# Modules:-Adding-a-Module

To add a [module](https://github.com/hicommonwealth/edgeware-node/wiki/Modules):

1. Add its github repo to:
   * [Cargo.toml](modules:Cargo.toml)
   * [node/runtime/Cargo.toml](modules:node/runtime/Cargo.toml)
   * [node/runtime/wasm/Cargo.toml](modules:node/runtime/wasm/Cargo.toml) \(be sure to have `default-features = false`\)
2. Changes to [the runtime](modules:node/runtime/src/lib.rs):
   * Add it as an `extern crate`.
   * Implement its `Trait` with production types.
   * Add it to the `construct_runtime` macro with all implemented components.
3. If its storage contains `config` elements, then you need to modify [the chain spec](modules:node/src/chain_spec.rs):
   * Add it to the `edgeware_runtime`'s list of `Config` types.
   * Add it to the `testnet_genesis` function, initializing all storage fields set to `config()`.
4. Build and run the chain.

