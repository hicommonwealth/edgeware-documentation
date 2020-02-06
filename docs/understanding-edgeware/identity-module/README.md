---
description: This page derived from the Polkadot Identity module page.
---

# Identity

Edgeware provides a naming system that allows participants to add personal information to their on-chain account and subsequently ask for verification of this information by [registrars](https://wiki.polkadot.network/docs/en/learn-identity#registrars).

### Setting an Identity

Users can register some default fields like legal name, display name, website, Twitter handle, Riot handle, etc. along with extra, custom fields for which they would like attestations \(see [Judgements](https://wiki.polkadot.network/docs/en/learn-identity#judgements)\). Users must reserve funds in a bond to store their information on chain - 10 KSM per identity, and 2.5 KSM per each field beyond the legal name. These funds are _locked_, not spent - they are returned when the identity is cleared. Each field can store up to 32 bytes of information, so the data must be less than that. When inputting the data manually through the [Extrinsics UI](https://polkadot.js.org/apps/#/extrinsics), a [UTF8 to bytes](https://onlineutf8tools.com/convert-utf8-to-bytes) converter can help.

{% page-ref page="adding-identities.md" %}



#### 

