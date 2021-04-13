---
uid: HistoryRecoveryConfiguration
---

# History recovery configuration

History recovery for PI adapters supports the following two scenarios:

- On demand history recovery operation - start and end time specification required.
- Limited (time-wise) automatic history recovery operation - backfills data gaps that originated from connection disruptions or PI adapter shutdown or both.

You can set the history recovery mode in the the **DataCollectionMode** parameter of your adapter's data source configuration. For more information, see the data source configuration topic.
