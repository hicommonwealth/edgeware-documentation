# Documentation Style Guide

## UI Support Section

There are many user-executable functions in Edgeware. It is helpful to note what interfaces support functions. Insert a single column table-list with hyperlinked names of the interfaces that support the function.

**Example:**

| Function Supported By: |
| :--- |
| [Polkadot UI](https://polkadot.js.org/apps/#/explorer) |
| [Commonwealth UI](http://commonwealth.im/) |
| [Polkascan](https://polkascan.io/pre/edgeware/dashboard) |
| [Polkassembly](https://polkassembly.io/) |

## Linking to Substrate Documentation

Where possible, insert a hint with the link to the appropriate Substrate.dev documentation page. Bold the text "Substrate Documentation" and insert a link.

**Example:**

{% hint style="info" %}
**Substrate Documentation** for[ Treasury Module](https://substrate.dev/rustdocs/master/pallet_treasury/index.html)
{% endhint %}

## Parameter Noting

Whenever documentation refers to a parameter modifiable through governance, a "hint" module should be used to highlight that parameter, describe in short the function, and assert the current parameter status. It should also be updated in the master parameter list. Bold the text "Parameter Note:"

**Example**

{% hint style="info" %}
**Parameter Note:** This hint block should name the parameter and state the current setting.
{% endhint %}

