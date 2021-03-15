# Running an Edgeware Node

<p>We want to provide a fast setup experience for you. If you have Docker, you can launch an Edgeware development node in a few seconds:</p>

<p><strong>Note</strong> If you don't have <a href="https://docs.docker.com/get-docker/">Docker installed, you can quickly install it from here</a></p>

<pre>
  <code>
git clone https://github.com/hicommonwealth/edgeware-node; cd edgeware-node/docker;
docker-compose up
  </code>
</pre>

<p><strong>Note:</strong> If you have run this command in the past, you probably want to purge your chain storage, so that you run through this tutorial with a clean slate. You can do this easily by using <code>docker-compose rm</code> to delete your existing docker volume.

<br>
</br>

<img src="https://user-images.githubusercontent.com/32852637/111100462-38007800-851e-11eb-887e-b35da08c8e70.png">

You should start to see blocks being produced by your node in your terminal.
  
You can interact with your node using the Polkadot UI:
  
<a href="https://polkadot.js.org/apps/">polkadot.js.org/apps/</a>
  



> **Note:** You will need to use a Chromium based browser (Google Chrome) to have this site interact with your local node. The Polkadot UI is hosted on a secure server, and your local node is not, which may cause compatibility issues on Firefox. The other option is to [clone and run the Polkadot UI locally](https://github.com/polkadot-js/apps). <br>

To point the UI to your local node, you need to adjust the **Settings.** Just select 'Local Node (127.0.0.1:9944)' from the endpoint dropdown: <br>

```
Click on the chain name > Development node/endpoint to connect to > Local Node (127.0.0.1:9944) > Switch
```

<img width="1514" alt="switch-to-localhost" src="https://user-images.githubusercontent.com/32852637/111102434-75670480-8522-11eb-9d23-e0f651e30fc9.png"> <br>

If you go into the **Explorer** tab of the UI, you should also see blocks being produced!

<img width="1514" alt="block-explorer-edgeware" src="https://user-images.githubusercontent.com/32852637/111102554-beb75400-8522-11eb-90d4-d17ab54faff8.png">
