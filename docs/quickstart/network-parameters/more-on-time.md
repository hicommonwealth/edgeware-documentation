---
description: Exact Runtime code specifying constants related to block time and production.
---

# More on Time

{% hint style="info" %}
This code is from [https://github.com/hicommonwealth/edgeware-node/blob/master/node/runtime/src/constants.rs](https://github.com/hicommonwealth/edgeware-node/blob/master/node/runtime/src/constants.rs)  
  
It may be out of date on this page, refer to the link above for most up to date runtime data.
{% endhint %}

```text
	pub const MILLISECS_PER_BLOCK: Moment = 6000;
	pub const SECS_PER_BLOCK: Moment = MILLISECS_PER_BLOCK / 1000;

	pub const SLOT_DURATION: Moment = MILLISECS_PER_BLOCK;

	// 1 in 4 blocks (on average, not counting collisions) will be primary BABE blocks.
	pub const PRIMARY_PROBABILITY: (u64, u64) = (1, 4);

	pub const EPOCH_DURATION_IN_BLOCKS: BlockNumber = 1 * HOURS;
	pub const EPOCH_DURATION_IN_SLOTS: u64 = {
		const SLOT_FILL_RATE: f64 = MILLISECS_PER_BLOCK as f64 / SLOT_DURATION as f64;

		(EPOCH_DURATION_IN_BLOCKS as f64 * SLOT_FILL_RATE) as u64
	};

	// These time units are defined in number of blocks.
	pub const MINUTES: BlockNumber = 60 / (SECS_PER_BLOCK as BlockNumber);
	pub const HOURS: BlockNumber = MINUTES * 60;
	pub const DAYS: BlockNumber = HOURS * 24;
```

{% embed url="https://github.com/hicommonwealth/edgeware-node/blob/master/node/runtime/src/constants.rs" %}



