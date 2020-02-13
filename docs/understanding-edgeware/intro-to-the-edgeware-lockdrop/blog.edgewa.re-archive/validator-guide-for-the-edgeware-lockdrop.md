---
description: 'Author: Drew Stone, written May 30 2019, archived from blog.edgewa.re'
---

# Validator Guide for the Edgeware Lockdrop

## Validator Guide for the Edgeware Lockdrop

If you understand [how to participate in the Edgeware Lockdrop,](https://blog.edgewa.re/edgeware-lockdrop-how-to-participate/) but want to nominate yourself as a validator at the launch of the Edgeware network, there is a short list of things you need to do first before completing the Lockdrop process. While this process doesn't guarantee that you will be a validator, it does enable your selection. At launch, Validators will be selected from the largest lock amounts from the set of nominated Edgeware Public Addresses.

#### SEE OUR OTHER ARTICLES ON THE LOCKDROP PROCESS: <a id="see-our-other-articles-on-the-lockdrop-process-"></a>

[Details on the Edgeware Lockdrop](https://blog.edgewa.re/full-details-on-the-edgeware-lockdrop/)

[Walkthrough: How to Participate in the Edgeware Lockdrop](https://blog.edgewa.re/edgeware-lockdrop-how-to-participate/)

[A guide to becoming a Validator through the Lockdrop](https://blog.edgewa.re/edgeware-lockdrop-for-validators/)

First, validators on Edgeware \(and Polkadot\) have _3_ keypairs: a hot wallet, a warm wallet, and a cold wallet. \(You can learn on this 3-keypair setup [here](https://slides.com/paritytech/validating-in-polkadot#/9).\)  To begin, we will generate:

* TWO sr25519 Edgeware Keypairs
* ONE ed25519 Edgeware Keypair

There are two ways to generate these keypairs. We encourage you to read both methods and choose the one you prefer. First, let's perform the pre-requisites to both methods:

#### PREREQUISITES <a id="prerequisites"></a>

1. Install the Rust programming language - [See a guide](https://doc.rust-lang.org/cargo/getting-started/installation.html)
2. Download the Subkey program using the following command within your command line interface \(CLI\):

```text
 ✗ cargo install --force --git https://github.com/paritytech/substrate subkey
```

Now we are ready to generate our keypairs.

### Method 1: Create Separate Mnemonics for Each Keypair <a id="method-1-create-separate-mnemonics-for-each-keypair"></a>

_Note: You will need to store 3 different mnemonics to have access and control over the funds and functions of these accounts._

This method uses the `subkey generate` command in three instances and returns your mnemonic phrases, your seed, your hex-encoded public key, and your public address. To reiterate, with each instance of this command, you want to securely record the results, otherwise you may lose control or access to these wallets. Notice that, because we need one keypair with a different parameter \(the ed25519 keypair,\) the last command is `subkey -e generate`

Once complete, you should have 3 phrases, 3 seeds, 3 public keys, and 3 addresses. The commands and the output will look like this \(minus the \# titles\):

```text
# SR25519 MNEMONIC KEYPAIR 1

✗ subkey generate
 Phrase `meadow clip planet heavy afford rifle viable bus fury satoshi blue impose` is account:
  Seed: 0x225967f0f82c4958179f9ba1c9b8823b0bc87fca650d7f3181bd2131f54276ec
  Public key (hex): 0xc2e973c4d848d25613141ef883bf97d35b513230427f52c56d2bf92bc4fa365c
  Address (SS58): 5GUGVkn5Zpfej7EC8WEsoJ38QFqu5cWvTx3WYFBKznLQkMAH

# SR25519 MNEMONIC KEYPAIR 2

✗ subkey generate
 Phrase `outer mixture phrase prepare beauty horse shift about story onion duty vacant` is account:
  Seed: 0x866c461e8a5b602c755f6babd442f36992238f8e1f604a022a7e753c8a8efdea
  Public key (hex): 0xfeba4989f1de5fe7aa911f9abed67742b93099701d4f9b0e07b8ac35e2f78131
  Address (SS58): 5HphMm6GrQzXw7ZP2UEXatKgusbhNLj7AhRdgmmCp4H9Hojz

# ED25519 MNEMONIC KEYPAIR 3

✗ subkey -e generate
Phrase `vacant paddle daring vacant rude release dutch morning cushion pledge traffic armor` is account:
  Seed: 0x6c38500811b6ea3a46214531adac0fe67e18ba543fc2fc17ceeccc2b155568be
  Public key (hex): 0x16ca51710516a648e016b00b8872cb37946dc1aabd531021d593e1d76604cf40
  Address (SS58): 5Cab1dV9g8hb2MrBcVUjCyFEJBqBWZZ4djHRE4pBYHbk4kyB
```

### Method 2: Create 1 mnemonic and derive keys <a id="method-2-create-1-mnemonic-and-derive-keys"></a>

_Note: You will only need to store the top level mnemonic for this approach._

As you will see below, we _reuse_ just one mnemonic to generate more keys by appending [a string](https://en.wikipedia.org/wiki/String_%28computer_science%29) to the mnemonic phrase. For instruction purposes, we recommend you append `stash` , `controller` and `authority` \(the names of the wallet's purposes\) but you can append _any_ string.

Step 1: run `subkey generate` and record the results.

Step 2: run `subkey inspect "YOUR MNEMONIC FROM STEP 1 IN QUOTEMARKS" //stash`  and record the results. This is the info for the stash wallet.

Step 2: run `subkey inspect "YOUR MNEMONIC FROM STEP 1 IN QUOTEMARKS" //controller`  and record the results.This is the info for the controller wallet.

Step 2: run `subkey -e inspect "YOUR MNEMONIC FROM STEP 1 IN QUOTEMARKS" //authority`  and record the results. This is the info for the authority wallet - make sure to notice and include the `-e` parameter in this step.

Ensure you create and submit **2** sr25519 and **1** ed25519 public keys when participating in the Edgeware Lockdrop. Your commands and output will look like this:

```text
# TOP LEVEL MNEMONIC KEYPAIR

✗ subkey generate
Phrase `hurt clay tide opera club scout cupboard silk bone erupt over melt` is account:
  Seed: 0x25fd11bb0ea205295acee6787c1a2f80c47c2fea2f21392f9cc809e58a1eb94a
  Public key (hex): 0x8a6098968a2412d96cf451fb9b3d330ee02041d3f4572e16e555297b04869b65
  Address (SS58): 5FC9AFQ8RysaCB8V2Sp93vVDT4asGymC6Y6jjaQpRKdAyN2o

# SR25519 DERIVED PUBLIC KEY 2 (notice the //stash)

✗ subkey inspect "hurt clay tide opera club scout cupboard silk bone erupt over melt"//stash
Secret Key URI `hurt clay tide opera club scout cupboard silk bone erupt over melt//stash` is account:
  Public key (hex): 0x807d3de39cf5cb33c54bf2f839711f9f776c0b3f140228a2edf1336f7ff65602
  Address (SS58): 5EyBC2h8qneTjAmZ7MW4MaPCnZxQAC23fTcx4pPMy6rjHtkE

# SR25519 DERIVED PUBLIC KEY 2 (notice the //controller)

✗ subkey inspect "hurt clay tide opera club scout cupboard silk bone erupt over melt"//controller
Secret Key URI `hurt clay tide opera club scout cupboard silk bone erupt over melt//controller` is account:
  Public key (hex): 0x403ac86021d47fc9df6e0a8fd27396393dc7dfd40722a09a7b31d99730eaf962
  Address (SS58): 5DWvPDgLia25EGk8Bm6B3b9Jm4Ym32f31SSEyLh1Yt2JPAe5

# ED25519 DERIVED KEYPAIR 3 (notice the -e and //authority)

✗ subkey -e inspect "hurt clay tide opera club scout cupboard silk bone erupt over melt"//authority
Secret Key URI `hurt clay tide opera club scout cupboard silk bone erupt over melt//authority` is account:
  Seed: 0x26b7b23056e3fe175354a7401777e358a231a3d4d7544431f824aa49b2171522
  Public key (hex): 0x26b7b23056e3fe175354a7401777e358a231a3d4d7544431f824aa49b2171522
  Address (SS58): 5CwUFDUYDsFMQAgW8DCFYRppX4BnNutNtRicULyEBGQRvtYi
```

3.   [Concatenate](https://en.wikipedia.org/wiki/Concatenation) the three `stash`, `controller` and `authority` public keys together, removing the `0x` in front of the controller and authority keys \(or 2nd and 3rd keys if you used different strings\) before concatenating them, leaving only one instance of `0x` at the beginning of the final string.

This final string should be 194 characters regardless of your choice of method.

**Example of Method 1 Concatenation \(3 separate mnemonics\):**

```text
0xc2e973c4d848d25613141ef883bf97d35b513230427f52c56d2bf92bc4fa365cfeba4989f1de5fe7aa911f9abed67742b93099701d4f9b0e07b8ac35e2f7813116ca51710516a648e016b00b8872cb37946dc1aabd531021d593e1d76604cf40
```

**Example of Method 2 Concatenation \(1 mnemonic\):**

```text
0x807d3de39cf5cb33c54bf2f839711f9f776c0b3f140228a2edf1336f7ff65602403ac86021d47fc9df6e0a8fd27396393dc7dfd40722a09a7b31d99730eaf96226b7b23056e3fe175354a7401777e358a231a3d4d7544431f824aa49b2171522
```

## Edgeware Lockdrop <a id="edgeware-lockdrop"></a>

When you are ready to participate in the lockdrop, you will submit that concatenation of your three public keys as your input into either the:

* The field labeled "EDG public key \(hex\)" in the [Lockdrop UI](https://blog.edgewa.re/edgeware-lockdrop-for-validators/edgewa.re/lockdrop) -or-
* If you are using the CLI, as your `--edgewarePublicKey`

Once you finalize your participation in the lockdrop, you are done - you have successfully submitted your intent and nomination to validate on the Edgeware network.  

### Questions? <a id="questions"></a>

Get help from the community and our team [in our Discord.](https://discord.gg/DEYTQGZ)

## Why? More on stash, controller and authority <a id="why-more-on-stash-controller-and-authority"></a>

In order for us to generate the genesis specification for the Edgeware chains, validators are identified by 3 keys: a stash \(sr25519\), controller \(sr25519\), and authority \(ed25519\) key.

1. Stash accounts control the stake and bond to controllers.
2. Controller accounts control staking settings
3. Authority accounts author blocks and more.

Therefore, when you participate in the lockdrop, we will need to have access to three keys per validating locker. With this, we can simply parse out the keys and setup the chain spec as intended.

