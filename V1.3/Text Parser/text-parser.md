---
uid: TextParser
---

# Text Parser

The adapter you are using includes the Text Parser component which ensures consistent parsing of text from different files. For more information on which file types are supported for your adapter, see the topics in this chapter.

Designed to be a document parser, the Text Parser parses a semantically complete document in its entirety.
The Text Parser produces OMF compatible output, which in turn is compatible with the OCS backing SDS (Sequential Data Store) that stores data in streams consisting of multiple values and indexes.

## Data types supported by the Text Parser

* DateTime
* DateTimeOffset
* TimeSpan
* sbyte
* byte
* short
* ushort
* int
* uint
* long
* ulong
* float
* double
* decimal
* bool
* char
* string

**Note:** Not all data types supported by the Text Parser are also supported by OMF.

## Culture support

Some numeric values and datetimes support cultures when they are being parsed. The default culture is `en-US (US English)` (InvariantCulture). OSIsoft recommends to leave the adapter at the default unless you expect culturally variant input.

**Note:** Installed cultures vary by machine with both Linux and Windows. If the specified culture is not installed, the text parser fails to parse input that requires that culture.

## Time zone support

A time zone or offset specified by a time is always used to convert to UTC time. Time zones are only used if there is no offset or time zone specifier in a text date and time string.

If a time zone supports time changes between daylight and standard times, the text file source might contain invalid or ambiguous datetimes. These are usually only possible for a two hour period each year because they occur during time changes. Ambiguous times are reported as standard times.
