# Edgeware Node

Blockchain networks are composed of individual **nodes** that are connected by a peer-to-peer \(P2P\) network. Nodes are the individual computers on a network running the blockchain software that makes everything work. The `Edgeware Node` subsection includes anything relevant to nodes on operating on Edgeware. 

### For node operators, validators, and other users

A getting started guide can be found at our [Github Wiki](https://github.com/hicommonwealth/edgeware-node/wiki), including guides for running a node, validating, and setting up basic monitoring tools to keep your node online.

### To start your node and connect to Wako v3.3.3

GitHub repository: https://github.com/edgeware-network/edgeware-node

For Mainnet, run: 
```text
docker run --rm -it decentration/edgeware:v3.3.3 edgeware --chain=edgeware --name <INSERT-NAME> --wasm-execution Compiled
```

For Beresheet testnet, run:
```text
docker run --rm -it decentration/edgeware:v3.3.3 edgeware --chain=beresheet --name <INSERT_NAME>
```
Docker image: https://hub.docker.com/r/decentration/edgeware/tags?page=1&ordering=last_updated



For any additional questions or information, refer to our `builders-general` channel in the [Edgeware Discord](https://discord.gg/zdFJm4gA5M).

{% page-ref page="../../quickstart/set-up-a-full-node.md" %}

{% page-ref page="../../development/develop/smart-contracts/evm-smart-contracts/tutorials/deploy-an-evm-contract/setting-up-a-edgeware-evm-node.md" %}

{% page-ref page="../../development/develop/smart-contracts/wasm-smart-contracts/tutorials/deploy-a-wasm-contract/running-an-edgeware-node.md" %}




