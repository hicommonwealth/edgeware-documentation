# Create an Edgeware Identity

## Identity

Substrate provides a naming system that allows participants to add personal information to their on-chain account and subsequently ask for verification of this information by registrars. [Learn more here](https://wiki.polkadot.network/docs/en/learn-identity#registrars)

## Adding Identities Using Polkadot.js

The easiest way to add the built-in fields is to click the gear icon next to one's account and select "Set on-chain identity".

![](https://user-images.githubusercontent.com/32852637/116119305-477def80-a68c-11eb-9dba-1124d54a13e7.PNG)

![](https://user-images.githubusercontent.com/32852637/116119319-4d73d080-a68c-11eb-9b4e-8ac906e18baf.png)

To add custom fields beyond the default ones, use the Extrinsics UI to submit a raw transaction by first clicking "Add Item" and adding any field name you like. The example below adds a field `steam` which is a user's [Steam](https://store.steampowered.com/) username. The first value is the field name in bytes \("steam"\) and the second is the account name in bytes \("theswader"\). The display name also has to be provided, otherwise the Identity pallet would consider it wiped if we submitted it with the "None" option still selected. That is to say, every time you make a change to your identity values, you need to re-submit the entire set of fields: the write operation is always "overwrite", never "append".

The rendering of such custom values is, ultimately, up to the UI/dapp makers. In the case of PolkadotJS, the team prefers to only show official fields for now. If you want to check that the values are still stored, use the [Chain State UI](https://polkadot.js.org/apps/#/chainstate) to query the active account's identity info:

![Raw values of custom fileds are available on-chain](https://wiki.polkadot.network/img/identity/05.jpg)

It is up to your own UI or dapp to then do with this data as it pleases. The data will remain available for querying via the Polkadot API, so you don't have to rely on the PolkadotJS UI.

You can have a maximum of 100 custom fields.

### Format Caveat

Please note the following caveat: because the fields support different formats, from raw bytes to various hashes, a UI has no way of telling how to encode a given field it encounters. The PolkadotJS UI currently encodes the raw bytes it encounters as UTF8 strings, which makes these values readable on screen. However, given that there are no restrictions on the values that can be placed into these fields, a different UI may interpret them as, for example, IPFS hashes or encoded bitmaps. This means any field stored as raw bytes will become unreadable by that specific UI. As field standards crystallize, things will become easier to use but for now, every custom implementation of displaying user information will likely have to make a conscious decision on the approach to take, or support multiple formats and then attempt multiple encodings until the output makes sense.

