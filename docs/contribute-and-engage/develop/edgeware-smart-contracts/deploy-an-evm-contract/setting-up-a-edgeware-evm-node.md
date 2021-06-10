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

![](https://user-images.githubusercontent.com/32852637/121593861-5afdd380-ca0a-11eb-80dd-8922a0b7cfc7.PNG)

Afterwards you can head to [Polkadot Apps](https://polkadot.js.org/apps/?rpc=ws%3A%2F%2F127.0.0.1%3A9944#/explorer) and connect to 127.0.0.1:9944, and you should see blocks being produced.

![](https://user-images.githubusercontent.com/32852637/121594313-e9725500-ca0a-11eb-8f5f-36e5184d6b46.PNG)

Now you can continue to connect [Metamask](https://main.edgeware.wiki/contribute-and-engage/develop/edgeware-smart-contracts/deploy-an-evm-contract/using-metamask), Remix, and Web3.js to have great experience.

## Reach us for more engagement

Glad you've made it through! 🥰 We are eager to guide your more on your exploration through Edgeware Ethereum compability feature. We are **keen to hear your experience and suggestions you may have for us.**. You can feel free to [chat with us in the Edgeware's channels like Discord, Element and Telegram](https://linktr.ee/edg_developers), we can help you out with issues you may have or project you may want to be funded through our [Treasury program](https://docs.edgewa.re/edgeware-runtime/treasury). Don't hesitate to share your feedback on our channels, there is always space to improve! 🙌

