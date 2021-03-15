# Creating an ink! Project

<p>We are going to use the ink! CLI to generate the files we need for a Substrate smart contract project.</p>

<p>Make sure you are in your working directory, and then run:</p>

<pre><code>cargo contract new flipper</code></pre>

<p>This command will create a new project folder named <code>flipper</code> which we will explore:</p>

<pre><code>cd flipper/</code></pre>

<h4>ink! Contract Project</h4>

<pre><code>
<p>flipper
|
.
├── Cargo.toml
└── lib.rs</p></code></pre>

<h2>Contract Source Code</h2>

<p>The ink CLI automatically generates the source code for the "Flipper" contract, which is about the simplest "smart" contract you can build. You can take a sneak peak as to what will come by looking at the source code here:</p>

<p><a href="https://github.com/hicommonwealth/ink/blob/master/examples/flipper/lib.rs">Flipper Example Source Code</p></a>
  
<p> The Flipper contract is nothing more than a <code>bool</code> which gets flipped from true to false through the <code>flip()</code> function. We won't go so deep into the details of this source code because we will be walking you through the steps to build a more advanced contract!
  
<h2>Testing Your Contract</h2>

<p>You will see at the bottom of the source code there is a simple test which verifies the functionality of the contract. We can quickly test that this code is functioning as expected using the <strong>off-chain test environment</strong> that ink! provides.</p>

<p>In your project folder run:</p>

<pre><code>cargo +nightly test</code></pre>

<p>To which you should see a successful test completion:</p>
