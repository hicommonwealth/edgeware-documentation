# Edgeware Node

Blockchain networks are composed of individual **nodes** that are connected by a peer-to-peer (P2P) network. Nodes are the individual computers on a network running the blockchain software that makes everything work. The `Edgeware Node` subsection includes anything relevant to nodes on operating on Edgeware.

## For node operators, validators, and other users

A getting started guide can be found at our [Github Wiki](https://github.com/hicommonwealth/edgeware-node/wiki), including guides for running a node, validating, and setting up basic monitoring tools to keep your node online.

## To start your node and connect to Wako v3.3.3

GitHub repository: [https://github.com/edgeware-network/edgeware-node](https://github.com/edgeware-network/edgeware-node)

For Mainnet, run:

```
docker run --rm -it decentration/edgeware:v3.3.3 edgeware --chain=edgeware --name <INSERT-NAME> --wasm-execution Compiled
```

For Beresheet testnet, run:

```
docker run --rm -it decentration/edgeware:v3.3.3 edgeware --chain=beresheet --name <INSERT_NAME>
```

For any additional questions or information, refer to our `builders-general` channel in the [Edgeware Discord](https://discord.gg/zdFJm4gA5M).

{% content-ref url="../../quickstart/set-up-a-full-node.md" %}
[set-up-a-full-node.md](../../quickstart/set-up-a-full-node.md)
{% endcontent-ref %}

{% content-ref url="../../development/develop/smart-contracts/evm-smart-contracts/tutorials/deploy-an-evm-contract/setting-up-a-edgeware-evm-node.md" %}
[setting-up-a-edgeware-evm-node.md](../../development/develop/smart-contracts/evm-smart-contracts/tutorials/deploy-an-evm-contract/setting-up-a-edgeware-evm-node.md)
{% endcontent-ref %}

{% content-ref url="../../development/develop/smart-contracts/wasm-smart-contracts/tutorials/deploy-a-wasm-contract/running-an-edgeware-node.md" %}
[running-an-edgeware-node.md](../../development/develop/smart-contracts/wasm-smart-contracts/tutorials/deploy-a-wasm-contract/running-an-edgeware-node.md)
{% endcontent-ref %}
