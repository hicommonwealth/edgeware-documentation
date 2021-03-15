# Setup Environment

To follow this tutorial, you will need to set up some stuff on your computer.
<br>
<h2>Substrate Prerequisites</h2>
<p>To get started, you need to make sure your computer is set up to build Substrate.

If you are using <strong>OSX</strong> or most popular <strong>Linux</strong> distros, you can do it by running:</p>

<pre><code>curl https://sh.rustup.rs -sSf | sh -s -- -y</code></pre>
<br>
<pre><code>rustup target add wasm32-unknown-unknown --toolchain stable
rustup component add rust-src --toolchain nightly
rustup toolchain install nightly-2020-06-01
rustup target add wasm32-unknown-unknown --toolchain nightly-2020-06-01</code></pre>

<br>

<p>The final tool we will be installing is the ink! command line utility which will make setting up Substrate smart contract projects easier.
</p>

<p>You can install the utility using Cargo with:</p>

<pre><code>cargo install --git https://github.com/hicommonwealth/cargo-contract cargo-contract --force</code></pre>

<p>You can then use <code>cargo contract --help</code> to start exploring the commands made available to you.

<hr>

<p><strong>Note:</strong> <i>The ink! CLI is under heavy development and some of its commands are not implemented, yet!</i>
