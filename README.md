# positive-search-timestamps

Daily fingerprints of the **[Positive Search](https://positivesearch.app)** index history, anchored in the Bitcoin blockchain.

**This repository contains no market data.** No index values, no articles, no links — only fingerprints and their timestamp proofs.

---

## Why

Positive Search publishes a live news-sentiment index for Bitcoin, gold and oil. Open sources answer for the present: every article behind a reading sits on the page with a link to the original.

The harder question is about the past — *was yesterday's number really that number?*

"Trust us" is a poor answer. This repository is the other one.

## What is here

```
heads/YYYY-MM-DD.json       fingerprint of the history as of that day
heads/YYYY-MM-DD.json.ots   its OpenTimestamps proof
```

A head file is small and dull on purpose:

```json
{
  "date": "2026-08-09",
  "chain_head": "ca785344c3661a0e7072170762b0a8733f805f432fb92c11b39decb9f6ed1896",
  "snapshots": 1540,
  "last_ts": "2026-08-09T11:46:27Z"
}
```

`chain_head` is a single 32-byte number the whole history folds into. Readings are appended to a log that can only be continued, and each entry carries the fingerprint of the one before it — so altering one past reading changes every entry after it, and the head stops matching what was stamped here.

## How to verify

```bash
pip install opentimestamps-client
ots verify heads/2026-08-09.json.ots
```

This reports the Bitcoin block the fingerprint was anchored in, and its time. Nothing about that depends on Positive Search, its host, or GitHub.

A fresh stamp reads `PendingAttestation` for an hour or two: the calendar has accepted the fingerprint, but the block has not been mined yet. That is expected — stamping and confirmation run as two separate jobs.

## What this proves — and what it does not

**Proven:** a record with this fingerprint existed no later than the moment it was stamped, and has not changed since.

**Not proven:** that the number itself is right. Timestamping answers for immutability, not for quality — quality is answered for by the open sources behind every reading, on the site.

The default branch rejects force-pushes and deletion. The proofs cannot be rewritten, including by us.

---

Questions: hi@positivesearch.app
