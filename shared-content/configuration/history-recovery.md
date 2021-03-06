---
uid: HistoryRecovery
---

# History recovery

History recovery for PI adapters supports the following two scenarios:

- On demand history recovery operation - start time or end time must be specified (or both). If either start or end time is not specified, the default is `utcnow`.
- Limited automatic history recovery operation - backfills data gaps that originated from connection disruptions, data source issues, or PI adapter shutdown or both. This is limited to a maximum time-range of four days.

You can set the history recovery mode in the the **DataCollectionMode** parameter of your adapter's data source configuration. For more information, see the data source configuration topic.
