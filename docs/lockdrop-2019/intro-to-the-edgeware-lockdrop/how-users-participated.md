---
description: This page is archived from blog.edgewa.re for posterity.
---

# How Users Participated

_**The Edgeware Lockdrop, was available to participate in from  June 1, 2019 - August 30, 2019.**_

For ease and clarity: the [mainnet Edgeware Lockdrop contract](https://etherscan.io/dapp/0x1b75b90e60070d37cfa9d87affd124bb345bf70a) is located at:

**Current**: `0xFEC6F679e32D45E22736aD09dFdF6E3368704e31`

OLD: `0x1b75b90e60070d37cfa9d87affd124bb345bf70a` **\(Do not use\)**

The Edgeware Lockdrop UI: http://edgewa.re/lockdrop

####  <a id="see-our-other-articles-on-the-lockdrop-process-"></a>

### **Participating in the Edgeware Lockdrop** <a id="participating-in-the-edgeware-lockdrop"></a>

\*\*Note: \*\*The Edgeware Lockdrop begins June 1, 2019 through August 30th, 2019. The following instructions are provided ahead of time in order to provide the best guidance and obtain feedback.

#### AN OVERVIEW OF THE SIMPLEST METHOD OF PARTICIPATION BY LOCKING: <a id="an-overview-of-the-simplest-method-of-participation-by-locking-"></a>

You will:

1. Generate Edgeware key/phrase
2. Enter your EDG public key/address into our interface
3. Select Your Desired Lock Period
4. Sign into Metamask
5. and finally send ETH to your unique Edgware Lockdrop User Contract \(LUC\).

**Test run?** There are Rosten testnet contracts you can experiment with now, but no guides to this have been published yet. [Hop in our Discord](https://discord.gg/7rFedPt) for help on those.Get notified when the Edgeware Lockdrop Opens

Let's first create a mnemonic and keypair using the secure method described below.

### Step 1: Creating an Edgeware Keypair <a id="step-1-creating-an-edgeware-keypair"></a>

**Note**: You can generate your keypair now to be prepared for June 1, and complete the remaining steps on or after that date.

A crucial part of the Edgeware Lockdrop is having Edgeware keys to lock or signal with. Therefore, we will first describe how to create an Edgeware keypair in one of two different options:

* The Edgeware Lockdrop UI \(User-friendly\)

OR

* Rust and the Subkey Program \(Requires using a command line interface \(CLI\)\)

#### OPTION 1: CREATING A KEYPAIR USING THE EDGEWARE LOCKDROP UI

If using a command line interface \(CLI\) is not your thing, then you can use the [Edgeware Lockdrop Keygen UI](https://edgewa.re/keygen/index.html). Don't forget to save the information in a secure place. If you lose the 12 string mnemonic, you will lose access to your funds.

#### OPTION 2: USING SUBKEY TO CREATE A KEYPAIR

This more secure process requires the Rust programming language and Cargo, the Rust package manager. Take this time to ensure you have both of these installed, if not, [install Rust and Cargo.](https://doc.rust-lang.org/cargo/getting-started/installation.html)

Once both Rust and Cargo are installed, complete the following:

1. Install `subkey` by running the following command in a shell like Bash or Terminal.

`cargo install --force --git https://github.com/paritytech/substrate subkey`

1. Run `subkey generate` to generate an sr25519 keypair and mnemonic. The following is an example of the output of this command:

```text
✗ subkey generate
Phrase `easy real wisdom valley box century leisure bounce coconut option mushroom cycle` is account:`
  Seed: 0xa60afef8639d74d6ba7d98d7638b8d51e3cb0f6e1c4a23549727609a593abf4d
  Public key (hex): 0xa469e40f0a073be5b28e2df6e746ce6519260cdd764bc5f6b3fb3aac5cda3c35
  Address (SS58): 5FnHAc3WEXdkkiFPciTvWnRNh5VBCaeGP8wdbtBtVM7iA4bL
```

Store your mnemonic somewhere secure, or you may lose access to your tokens.

We will use the following public key \_as an example \_ to participate in the Edgeware Lockdrop. \(USE THE ONE YOU GENERATE!\):

`0xa469e40f0a073be5b28e2df6e746ce6519260cdd764bc5f6b3fb3aac5cda3c35`

### Step 2: Create your LUC, 'Lockdrop User Contract' <a id="step-2-create-your-luc-lockdrop-user-contract-"></a>

The following options are geared towards less technical users for Options 1 and 2, and more technical users for Option 3.

First, open the [Edgeware Lockdrop site](https://edgewa.re/lockdrop).

**Option 1. Use Metamask Online \(User-Friendliest\)**  
The website supports Metamask and the logic can be verified here. Additionally, for Ledger users, there is [Ledger support on Metamask](https://medium.com/metamask/metamask-now-supports-ledger-hardware-wallets-847f4d51546).

**Option 2. Use MyCrypto Online \(User-Friendlier\)**  
Click the MyCrypto option will display some instructions for locking or signaling on the Edgeware Lockdrop contract. Additionally, the UI will display the transaction data that you will need to paste into MyCrypto interface. You can check that the calculation of the transaction data here. **Trying this Offline?** If attempting to use MyCrypto offline, it may fail, as the contract module requires nonce and data from a recent block. This issue can be avoided by using [Parity Signer with MyCrypto.](https://www.parity.io/send-transactions-with-mycrypto-beta-and-parity-signer/)

If you've opted for one of these two options, you are all set - congratulations! If you've chosen the CLI, the rest of this article is for you.

**\(Expert\) Option 3: Using the Edgeware-Lockdrop CLI \(Most Secure\)**  
The final option you can use is our command line interface. This option should be used if you don't want to participate with a web browser. In order to use this option, you must have access to the hex-encoded private key containing the funds you want to lock or signal from.

For this option, once you have the hex-encoded private keys to your ETH, follow these steps:

#### CLI: SETUP YOUR EXECUTION <a id="cli-setup-your-execution"></a>

Clone the repo with `https://github.com/hicommonwealth/edgeware-lockdrop`

Install the `node_modules` with `yarn`

Create a file named `.env` with the following format:

```text
# ETH config
ETH_PRIVATE_KEY=0xHEXOFPRIVATEKEY

# Node/provider config
INFURA_PATH=https://ropsten.infura.io/v3/<INFURA_API_KEY>

# Lockdrop config
LOCKDROP_CONTRACT_ADDRESS=0xLOCKDROP

# Edgeware config
EDGEWARE_PUBLIC_KEY=0xa469e40f0a073be5b28e2df6e746ce6519260cdd764bc5f6b3fb3aac5cda3c35
```

### CLI: LOCK OR SIGNAL

#### **Locking via Command Line Interface**

{% hint style="info" %}
**The Command Line Interface \(CLI\) has been deprecated. These instructions are retained for posterity.** 
{% endhint %}

Locking with the CLI is done with the flag -l. In order to lock successfully, you need to specify the following flags:

`-l` - lock in the Edgeware Lockdrop  
`—lockLength <length>` - the integer length of the term to lock: 3, 6, or 12 months  
`—lockValue <value>` - the integer or decimal amount of value to lock up  
\(OPTIONAL\) `—edgewarePublicKey <publicKey>` - the hex encoded Edgeware public key \(Include an Edgeware public key if one is not provided in the `.env` file. If you are validating, you MUST submit 2 SR25519 and 1 ed25519 keys concatenated\)  
\(OPTIONAL\) `—isValidator` - if present, indicates the intent to be a validator

**Examples:**

Locking up 1 ETH for 3 months with no intent to validate.

```text
node scripts/lockdrop.js -l --lockValue 1 --lockLength 3 --edgewarePublicKey 0xa469e40f0a073be5b28e2df6e746ce6519260cdd764bc5f6b3fb3aac5cda3c35
```

Locking up 0.025 ETH for 12 months with no intent to validate.

```text
node scripts/lockdrop.js -l --lockValue 0.025 --lockLength 12 --edgewarePublicKey 0xa469e40f0a073be5b28e2df6e746ce6519260cdd764bc5f6b3fb3aac5cda3c35
```

Locking up 1 ETH for 3 months and indicating intent to validate. _If you are validating you MUST create and concatenate 2 SR25519 and 1 ED25519 public keys in that order._

```text
node scripts/lockdrop.js -l --lockValue 1 --lockLength 3 --isValidator --edgewarePublicKey 0x9e8f2c6c9b0a4ef5d3c4c524b0f49d7ac60f10a3b0649ff45c0f273420a34732fe1c6e6fd4ecee1cb391f58131ac91ea2debe06d7124564f2e5a03506fbd926dfb6eed2b4afc7284e6ab23f3a55d799a5cf2c64cf2f398f6eb11be5124a3ccfa
```

#### **CLI: Signaling via Command Line Interface**

Signaling with the CLI is done with the flag `-s`. In order to signal successfully, you need to specify the following flags.

`-s <contractAddress>`- signal from any Ethereum address in the Edgeware Lockdrop  
`-n <nonce>`- the nonce used to create the contract from the private key in the file named .env  
\(OPTIONAL\) `—edgePublicKey <publicKey>`- the hex encoded Edgeware public key \(Include an Edgeware public key if one is not provided in the `.env` file\)

**Examples:**

Signaling with the same Ethereum address as corresponds to the local private key hex.

```text
node scripts/lockdrop.js -s 0x2d65a140446894Ef1E71C333ecaA5BD8b5e6D568 --edgewarePublicKey 0xa469e40f0a073be5b28e2df6e746ce6519260cdd764bc5f6b3fb3aac5cda3c35
```

Signaling with a contract that was created using the local private key hex.

```text
node scripts/lockdrop.js -s 0xc79cb8BEEdA12595Db8Afcfd558931B33d64Cdb1 -n 101 --edgewarePublicKey 0xa469e40f0a073be5b28e2df6e746ce6519260cdd764bc5f6b3fb3aac5cda3c35
```

On successful locking or signaling, you should see the transaction hash printed into the shell so that you can check the existence of this transaction on Ethereum block explorers. Additionally, you can use other functions in the CLI to get information about the locks you have now created.

The full CLI option list is:

```text
Options:
  -V, --version                     output the version number
  -b, --balance                     Get the total balance across all locks
  -l, --lock                        Lock ETH with the lockdrop
  -s, --signal <contractAddress>    Signal a contract balance in the lockdrop
  -n, --nonce <nonce>               Transaction nonce that created a specific contract address
  -u, --unlock <contractAddress>    Unlock ETH from a specific lock contract
  -r, --remoteUrl <url>             The remote URL of an Ethereum node (defaults to localhost:8545)
  --unlockAll                       Unlock all locks from the locally stored Ethereum address
  --lockdropContractAddress <addr>  The Ethereum address for the target Lockdrop (THIS IS A LOCKDROP CONTRACT)
  --allocation                      Get the allocation for the current set of lockers
  --ending                          Get the remaining time of the lockdrop
  --lockLength <length>             The desired lock length - (3, 6, or 12)
  --lockValue <value>               The amount of Ether to lock
  --edgewarePublicKey <publicKey>   Edgeware Public Key
  --isValidator                     A boolean flag indicating intent to be a validator
  --locksForAddress <userAddress>   Returns the history of lock contracts for a participant in the lockdrop
  -h, --help                        output usage information
```

