---
uid: System
---

# System

The Diagnostics.System dynamic type includes the following values which are logged in a stream with the id System.Diagnostics.
This diagnostic stream contains system level information related to the host platform that the adapter is running on.

| Property                            | Type       | Description                                                                       |
| ----------------------------------- | ---------- | --------------------------------------------------------------------------------- |
| timestamp                           | `string` | Timestamp of event                                                                |
| ProcessIdentifier                   | `int`    | Process id of the host process                                                    |
| StartTime                           | `string` | Time at which the host process started                                            |
| WorkingSet                          | `long`   | Amount of physical memory in bytes, allocated for the host process                |
| TotalProcessorTime (uom=s)          | `double` | Total processor time for the host process expressed in seconds                    |
| TotalUserProcessorTime (uom=s)      | `double` | User processor time for the host process expressed in seconds                     |
| TotalPrivilegedProcessorTime (uom=s)| `double` | Privileged processor time for the host process expressed in seconds               |
| ThreadCount                         | `int`    | Number of threads in the host process                                             |
| HandleCount                         | `int`    | Number of handles opened by the host process                                      |
| ManagedMemorySize (uom=MB)          | `double` | Number of bytes currently thought to be allocated in managed memory               |
| PrivateMemorySize (uom=MB)          | `double` | Amount of paged memory, in bytes, allocated for the host process                  |
| PeakPagedMemorySize (uom=MB)        | `double` | Maximum amount of memory in the virtual memory paging file, in bytes, used by the host process.|
| StorageTotalSize (uom=MB)           | `double` | Total size of the storage medium in use by the system                             |
| StorageFreeSpace (uom=MB)           | `double` | Free space available                                                              |

Each adapter component produces its own diagnostics streams.
