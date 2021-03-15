# Building Your Contract

<p>Run the following command to compile your smart contract:</p>

<pre><code>cargo +nightly contract build</code></pre>

<p>This special command will turn your ink! project into a Wasm binary which you can deploy to your chain. If all goes well, you should see a <code>target</code> folder which contains this <code>.wasm</code> file.</p>

<pre>
  <code>
  target
  └── flipper.wasm
  </code>
</pre>

<h2>Contract Metadata</h2>

<p>By running the next command we'll generate the contract metadata (a.k.a. the contract ABI):</p>

<pre><code>cargo +nightly contract generate-metadata</code></pre>

<p>You should have a new JSON file (<code>metadata.json</code>) in the same target directory:
  
<pre>
  <code>
  target
  ├── flipper.wasm
  └── metadata.json
  </code>
</pre>

<p>Let's take a look at the structure inside:</p>

<pre>
  <code>
  {
  "metadataVersion": "0.1.0",
  "source": {
    "hash": "0x11ba777b3457bf64cb99421786c90d421afde1c56579aa3dae336e58ccc8f783",
    "language": "ink! 3.0.0-rc1",
    "compiler": "rustc 1.47.0-nightly"
  },
  "contract": {
    "name": "flipper",
    "version": "0.1.0",
    "authors": [
      "[your_name] <[your_email]>"
    ]
  },
  "spec": {
    "constructors": [
      {
        "args": [
          {
            "name": "init_value",
            "type": {
              "displayName": [
                "bool"
              ],
              "type": 1
            }
          }
        ],
        "docs": [
          " Constructor that initializes the `bool` value to the given `init_value`."
        ],
        "name": [
          "new"
        ],
        "selector": "0xd183512b"
      },
      {
        "args": [],
        "docs": [
          " Constructor that initializes the `bool` value to `false`.",
          "",
          " Constructors can delegate to other constructors."
        ],
        "name": [
          "default"
        ],
        "selector": "0x6a3712e2"
      }
    ],
    "docs": [],
    "events": [],
    "messages": [
      {
        "args": [],
        "docs": [
          " A message that can be called on instantiated contracts.",
          " This one flips the value of the stored `bool` from `true`",
          " to `false` and vice versa."
        ],
        "mutates": true,
        "name": [
          "flip"
        ],
        "payable": false,
        "returnType": null,
        "selector": "0xc096a5f3"
      },
      {
        "args": [],
        "docs": [
          " Simply returns the current value of our `bool`."
        ],
        "mutates": false,
        "name": [
          "get"
        ],
        "payable": false,
        "returnType": {
          "displayName": [
            "bool"
          ],
          "type": 1
        },
        "selector": "0x1e5ca456"
      }
    ]
  },
  "storage": {
    "struct": {
      "fields": [
        {
          "layout": {
            "cell": {
              "key": "0x0000000000000000000000000000000000000000000000000000000000000000",
              "ty": 1
            }
          },
          "name": "value"
        }
      ]
    }
  },
  "types": [
    {
      "def": {
        "primitive": "bool"
      }
    }
  ]
}
  </code>
    </pre>

<p>You can see that this file describes all the interfaces that can be used to interact with your contract.</p>

  <ul>
  <li>Registry provides the <strong>strings</strong> and custom <strong>types</strong> used throughout the rest of the JSON.</li>
  <li>Storage defines all the <strong>storage</strong> items managed by your contract and how to ultimately access them.</li>
  <li>Contract stores information about the callable functions like <strong>constructors</strong> and <strong>messages</strong> a user can call to interact with your contract.     It also has helpful information like the <strong>events/strong> that are emitted by the contract or any <strong>docs.</strong></li>
  </ul>
  
  <br>
  
  <p>If you look close at the constructors and messages, you will also notice a <code>selector</code> which is a 4-byte hash of the function name and is used to route your contract calls to the correct functions.
  
 <hr>
 
 <p><strong>Learn More</strong></p>
 
 <p>ink! provides a built-in overflow protection enabled on our <code>Cargo.toml</code> file. It is recommended to keep it enabled to prevent potential overflow errors in your contract.</p>
 
 <pre>
  <code>
    [profile.release]
    panic = "abort"           <-- Panics shall be treated as aborts: reduces binary size
    lto = true                <-- enable link-time-optimization: more efficient codegen
    opt-level = "z"           <-- Optimize for small binary output
    overflow-checks = true    <-- Arithmetic overflow protection
  <code>
 </pre>
 
 <hr>

  








