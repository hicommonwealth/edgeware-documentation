# Waffle

![](../../../../../../../.gitbook/assets/wafflelogo.png)

 [Waffle](https://www.getwaffle.io) is a popular development framework for testing Solidity smart contracts. Since Edgeware is Ethereum compatible, with a few lines of extra configuration, you can use Edgeware as you normally would with Ethereum to develop on Edgeware.

### Configure Waffle to Connect to Edgeware <a href="configure-waffle-to-connect-to-moonbeam" id="configure-waffle-to-connect-to-moonbeam"></a>

Assuming you already have a JavaScript or TypeScript project, install Waffle:

```
npm install ethereum-waffle
```

To configure Waffle to run tests against a Edgeware development node or the Edgeware Beresheet Testnet, within your tests create a custom provider and add network configurations:

{% tabs %}
{% tab title="Javascript" %}
describe ('Test Contract', () => { // Use custom provider to connect to Beresheet or Edgeware development node const BeresheetProvider = new ethers.providers.JsonRpcProvider(('[https://beresheet2.edgewa.re/evm](https://beresheet2.edgewa.re/evm)')(Alternatively, one can use [https://beresheetX.edgewa.re/evm](https://beresheetx.edgewa.re/evm) where X can be any number from 1 to 8.); 

const devProvider = new ethers.providers.JsonRpcProvider('[http://localhost:9933/](http://localhost:9933)'); })
{% endtab %}

{% tab title="Typescript" %}
describe ('Test Contract', () => { // Use custom provider to connect to Beresheet or Edgeware development node const BeresheetProvider: Provider = new ethers.providers.JsonRpcProvider(('[https://beresheet2.edgewa.re/evm](https://beresheet2.edgewa.re/evm)')(Alternatively, one can use [https://beresheetX.edgewa.re/evm](https://beresheetx.edgewa.re/evm) where X can be any number from 1 to 8.); 

const devProvider: Provider = new ethers.providers.JsonRpcProvider('[http://localhost:9933/](http://localhost:9933)'); })
{% endtab %}
{% endtabs %}
