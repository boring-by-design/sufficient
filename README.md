Subject: A Small, Boring System That Makes a Point

We built a small system using two old Android 4.4 (KitKat) phones.

One device records continuous white noise in 5 minute 5 second blocks.
Each block overlaps the previous one by 5 seconds.
Files are compressed (AMR 4.75 kbps target), encrypted with AES using a per-chunk session key, and sent to a second device.

The private key is not stored on either device.

The receiving device stores the encrypted files on a 64GB SD card using a rolling FIFO window.
At ~200 KB per 5-minute block, this provides roughly three years of continuous storage.

Both devices run background-only APKs under 30 KB in size.
Data transfer is handled by Syncthing.
There is no cloud service, no analytics, no telemetry.

Power consumption:

* Sender: ~0.007 kWh per 24h (<1W)
* Receiver: ~0.006 kWh per 24h (<1W)

The entire system runs continuously for under 2 watts total.

This is not a product.
It is not optimized.
It is not modern.

It simply demonstrates that:

• Continuous recording
• Deterministic chunking
• Strong encryption
• Peer-to-peer transfer
• Multi-year rolling storage

can be achieved with obsolete hardware, minimal software, and negligible power consumption.

Sometimes constraint is clearer than innovation.

That is the point.
