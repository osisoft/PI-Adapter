---
uid: AutomaticHistoryRecovery
---

# Automatic history recovery

Besides on-demand history recovery, the PI adapter also supports automatic history recovery.

For automatic history recovery, the adapter keeps track of the components' **DeviceStatus** change to keep track of a list of periods to recover per component. The device states `DeviceInError` and `Stopping` are triggers for starting a new history recovery interval for a component. Once the device status is `Good`, the adapter closes the active interval and triggers the history recovery method in the adapter code. For more information, see also [Device status](xref:DeviceStatus).

**Note:** If the data collection mode is set to `CurrentWithBackfill`, the adapter clears periods not recovered for the component and stops keeping track of them. Only if the data collection mode is set to `HistoryOnly`, an automatic history recovery operation in progress will be canceled, otherwise it will be finished.