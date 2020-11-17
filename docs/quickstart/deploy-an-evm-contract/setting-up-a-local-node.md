### Setting up a Edgeware Node for Ethereum/EVM development

This guide walks you through setting up an Edgeware node with Ethereum/EVM compatibility.

> **Note** This is a fast-track way to run a node. [You can always compile from source](https://github.com/hicommonwealth/edgeware-node/tree/edgeware-frontier) as well. We recommend using your own compiled binaries for production mainnet.

> **Note** If you don't have [Docker installed, you can quickly install it from here](https://docs.docker.com/get-docker/)

You can clone our repo with docker-compose to get started right away:

```shell
git clone https://github.com/yangwao/substrate_playground; cd substrate_playground;
docker-compose -f edgeware_frontier.yml up
```
> **Note** If you want to reset or purge the local chain, delete the docker container by running `docker-compose -f edgeware_frontier.yml rm`

You will see something like this:

![Running-Edgeware-EVM-node](./assets/node-setup-run.png)

Afterwards you can head to [Polkadot Apps](https://polkadot.js.org/apps/?rpc=ws%3A%2F%2F127.0.0.1%3A9944#/explorer) and connect to 127.0.0.1:9944, and you should see blocks being produced.

![Edgeware-EVM-producing-blocks](./assets/frontier-explorer.png)

Now you can continue to connect [Metamask](4/interacting-with-a-Edgeware-node-using-metamask.md), Remix, and Web3.js to have great experience.

### Reach us for more engagement

Glad you've made it through! 🥰 We are eager to guide your more on your exploration through Edgeware Ethereum compability feature. We are **keen to hear your experience and suggestion you may for us.**. You can feel free to [chat with us in the Edgeware's channels like Discord, Element and Telegram](https://linktr.ee/edg_developers), we can help you out with issues you may have or project you may want to be funded through our [Treasury program](https://docs.edgewa.re/edgeware-runtime/treasury). Don't hesitate to share your feedback on our channels, there is always space to improve! 🙌
