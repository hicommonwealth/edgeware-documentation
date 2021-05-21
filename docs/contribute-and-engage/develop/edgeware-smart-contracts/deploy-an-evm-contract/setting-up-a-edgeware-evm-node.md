# Setting up an Edgeware EVM node

## Setting up a Edgeware Node for Ethereum/EVM development <a id="setting-up-a-edgeware-node-for-ethereumevm-development"></a>

This guide walks you through setting up an Edgeware node with Ethereum/EVM compatibility.

{% hint style="info" %}
**Note** This is a fast-track way to run a node. [You can always compile from source](https://github.com/hicommonwealth/edgeware-node/tree/v3.2.0) as well. We recommend using your own compiled binaries for production mainnet.
{% endhint %}

{% hint style="info" %}
**Note** If you don't have [Docker installed, you can quickly install it from here](https://docs.docker.com/get-docker/)
{% endhint %}

You can clone our repo with docker-compose to get started right away:

```text
git clone https://github.com/hicommonwealth/edgeware-node; cd edgeware-node/docker;
docker-compose up
```

{% hint style="info" %}
**Note** If you want to reset or purge the local chain, delete the docker container by running **`docker-compose rm`**
{% endhint %}

You will see something like this:

![Running-Edgeware-EVM-node](https://contracts.edgewa.re/4/assets/node-setup-run.png)

Afterwards you can head to [Polkadot Apps](https://polkadot.js.org/apps/?rpc=ws%3A%2F%2F127.0.0.1%3A9944#/explorer) and connect to 127.0.0.1:9944, and you should see blocks being produced.

![Edgeware-EVM-producing-blocks](https://contracts.edgewa.re/4/assets/frontier-explorer.png)

Now you can continue to connect [Metamask](https://contracts.edgewa.re/#/4/interacting-with-a-Edgeware-node-using-metamask), Remix, and Web3.js to have great experience.

## [Reach us for more engagement](https://contracts.edgewa.re/#/4/setting-up-a-local-node?id=reach-us-for-more-engagement) <a id="reach-us-for-more-engagement"></a>

Glad you've made it through! 🥰 We are eager to guide your more on your exploration through Edgeware Ethereum compability feature. We are **keen to hear your experience and suggestions you may have for us.**. You can feel free to [chat with us in the Edgeware's channels like Discord, Element and Telegram](https://linktr.ee/edg_developers), we can help you out with issues you may have or project you may want to be funded through our [Treasury program](https://docs.edgewa.re/edgeware-runtime/treasury). Don't hesitate to share your feedback on our channels, there is always space to improve! 🙌

