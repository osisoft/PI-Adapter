---
uid: ErrorRate
---

# Error rate

The Diagnostics.Adapter.ErrorRate dynamic type includes these values, which are logged in a stream with the id {componentid}.ErrorRate.

| Property  | Type   | Description                                              |
| --------- | ------ | -------------------------------------------------------- |
| timestamp | `string` | Timestamp of event                                       |
| ErrorRate | `double` | 1-minute rolling average of error rate (streams/second)	|
