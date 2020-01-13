# Developing on Edgeware

## Implemented Modules

* [Identity](https://github.com/hicommonwealth/edgeware-node/tree/master/modules/edge-identity)
* [Voting](https://github.com/hicommonwealth/edgeware-node/tree/master/modules/edge-voting)
* [Signaling](https://github.com/hicommonwealth/edgeware-node/tree/master/modules/edge-signaling)
* [TreasuryReward](https://github.com/hicommonwealth/edgeware-node/tree/master/modules/edge-treasury-reward)

## Adding A Module

1. Add its github repo to:
   * [Cargo.toml](Cargo.toml)
   * [node/runtime/Cargo.toml](node/runtime/Cargo.toml)
   * [node/runtime/wasm/Cargo.toml](node/runtime/wasm/Cargo.toml) \(be sure to have `default-features = false`\)
2. Changes to [the runtime](node/runtime/src/lib.rs):
   * Add it as an `extern crate`.
   * Implement its `Trait` with production types.
   * Add it to the `construct_runtime` macro with all implemented components.
3. If its storage contains `config` elements, then you need to modify [the chain spec](node/service/src/chain_spec.rs):
   * Add it to the `edgeware_runtime`'s list of `Config` types.
   * Add it to the `testnet_genesis` function, initializing all storage fields set to `config()`.
4. Build and run the chain.

