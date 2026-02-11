# Sufficient

*A small, boring system that makes a point.*

---

## Overview

This project demonstrates that:

- Continuous recording  
- Deterministic chunking  
- Strong encryption  
- Peer-to-peer transfer  
- Multi-year rolling storage  

can be achieved using:

- Two obsolete Android 4.4 (KitKat, API 19) phones  
- Background-only APKs under 30 KB  
- Open-source tools  
- Less than 2 watts total power  

No cloud.  
No telemetry.  
No analytics.  
No subscriptions.

Just constraint.

---

## The System

### Sender (Android 4.4)

- Records continuous **white noise only**
- Splits into **5 minute 5 second** blocks
- 5 second overlap ensures deterministic file transition
- Target codec: **AMR 4.75 kbps**
- Target file size: **< 200 KB per 5-minute block**
- Encrypts each block using:
  - Per-chunk AES session key
  - Public key wrapping
- Sends encrypted files to Receiver

**APK size:** ~30 KB

---

### Receiver (Android 4.4)

- Receives encrypted files
- Moves and stores them
- Maintains FIFO rolling storage on SD card
- 64 GB SD card ≈ **~3 years continuous storage**

**APK size:** ~20 KB

Data transport handled by **Syncthing (open source)**.

---

## Storage Math

AMR @ 4.75 kbps:

- ~178 KB per 5 minutes  
- ~2.4 MB per hour  
- ~57 MB per day  
- ~21 GB per year  
- ~63 GB ≈ 3 years  

No compression tricks.  
No deduplication.  
Just arithmetic.

---

## Power Consumption

Measured using inline USB meters and Tapo P110 smart plugs.

| Device   | 24h Consumption | Approx Power |
|-----------|----------------|--------------|
| Sender    | 0.007 kWh     | < 1 W        |
| Receiver  | 0.006 kWh     | < 1 W        |

**Total system draw:** under 2 watts continuous.

For obsolete hardware.

---

## Encryption Model

Each 5-minute block:

1. Generate random AES-256 session key  
2. Encrypt audio block (AES-GCM)  
3. Encrypt session key using embedded public key  
4. Transmit:
   - Ciphertext  
   - Wrapped session key  
   - Nonce  

Private key is **not stored on either device**.

Compromise of a device yields:
- Encrypted white noise
- No decryption capability

---

## Why Android 4.4?

Because it works.

- Deterministic behavior  
- No background execution limits  
- No forced cloud coupling  
- No silent system updates  
- No modern “helpfulness”  

Old hardware.  
Known behavior.  
Minimal surface area.

---

## Build Philosophy

Both APKs are:

- Built using free tools  
- Reproducible  
- Small enough to audit  
- Simple enough to understand  

It is possible to build Android APKs using nothing but a browser, even from another Android device.

That moment when it compiles cleanly and installs:

> "Look Ma — no hands."

---

## This Is Not

- A product  
- A surveillance tool  
- A cloud platform  
- An IoT startup  
- A pitch deck  

It is a demonstration.

---

## The Point

Security is not novelty.  
Resilience is not complexity.  
Innovation is not required for sufficiency.

Sometimes:

Constraint > sophistication  
Determinism > feature count  
Boring > clever  

That is all.
