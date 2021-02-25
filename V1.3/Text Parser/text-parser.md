---
uid: TextParser
---

# Text Parser

The adapter you are using includes the Text Parser component which ensures consistent parsing of text from XML, JSON, and CSV files. Designed to be a document parser, the Text Parser parses a semantically complete document in its entirety.

The Text Parser produces OMF compatible output, which in turn is compatible with the OCS backing SDS (Sequential Data Store) that stores data in streams consisting of multiple values and indexes.

**Note:** Not all data types supported by the Text Parser are also supported by OMF.

## Culture support

Some numeric values and datetimes support cultures when they are being parsed. The default culture is `en-US (US English)` (InvariantCulture). OSIsoft recommends to leave the adapter at the default unless you expect culturally variant input.

**Note:** Installed cultures vary by machine with both Linux and Windows. If the specified culture is not installed, the text parser fails to parse input that requires that culture.

## Time zone support

A time zone or offset specified by a time is always used to convert to UTC time. Time zones are only used if there is no offset or time zone specified in a text date and time string.

If a time zone supports time changes between daylight and standard times, the text file source might contain invalid or ambiguous datetimes. These are usually only possible for a two hour period each year because they occur during time changes. Ambiguous times are reported as standard times.

## Syntaxes for value retrieval

For information on which semantics are used for retrieving values, see the following documentation:

- XML - [XML Path Language (XPath)](https://www.w3.org/TR/1999/REC-xpath-19991116/)
- JSON - [JSONPath - XPath for JSON](https://goessner.net/articles/JsonPath/)
- CSV - Column Index (1 based) or Header value (if header defined)

The following syntaxes are used to extract values from documents.

### XML - Simple XPath example

```xml
<values>
  <value>
    <time>2020-08-10T12:10:46.0928791Z</time>
    <value>1.234567890</value>
  </value>
  <value>
    <time>2020-08-10T12:10:47.0928791Z</time>
    <value>12.34567890</value>
  </value>
  <value>
    <time>2020-08-10T12:10:48.0928791Z</time>
    <value>123.4567890</value>
  </value>
  <value>
    <time>2020-08-10T12:10:49.0928791Z</time>
    <value>1234.567890</value>
  </value>
  <value>
    <time>2020-08-10T12:10:50.0928791Z</time>
    <value>12345.67890</value>
  </value>
  <value>
    <time>2020-08-10T12:10:51.0928791Z</time>
    <value>123456.7890</value>
  </value>
  <value>
    <time>2020-08-10T12:10:52.0928791Z</time>
    <value>12345678.90</value>
  </value>
  <value>
    <time>2020-08-10T12:10:53.0928791Z</time>
    <value>123456789.0</value>
  </value>
</values>
```

### JSON - Simple JSONPath example

```json
[
  {
    "time": "2020-08-10T12:10:46.0928791Z",
    "value": 1.234567890
  },
  {
    "time": "2020-08-10T12:10:47.0928791Z",
    "value": 12.34567890
  },
  {
    "time": "2020-08-10T12:10:48.0928791Z",
    "value": 123.4567890
  },
  {
    "time": "2020-08-10T12:10:49.0928791Z",
    "value": 1234.567890
  },
  {
    "time": "2020-08-10T12:10:50.0928791Z",
    "value": 12345.67890
  },
  {
    "time": "2020-08-10T12:10:51.0928791Z",
    "value": 123456.7890
  },
  {
    "time": "2020-08-10T12:10:52.0928791Z",
    "value": 12345678.90
  },
  {
    "time": "2020-08-10T12:10:53.0928791Z",
    "value": 123456789.0
  }
]
```

### JSON - Complex JSONPath example

```json
{
  "StreamData": {
    "TPPrototype.uflsample.value_time": [
      {
        "StreamId": "TPPrototype.uflsample.value_time",
        "DataType": "Double",
        "Timestamp": "2013-12-01T06:00:00Z",
        "Value": 339.0
      },
      {
        "StreamId": "TPPrototype.uflsample.value_time",
        "DataType": "Double",
        "Timestamp": "2013-12-01T07:00:00Z",
        "Value": 344.0
      },
      {
        "StreamId": "TPPrototype.uflsample.value_time",
        "DataType": "Double",
        "Timestamp": "2013-12-01T17:00:00Z",
        "Value": 341.0
      }
    ],
    "TPPrototype.uflsample.value_timeString": [
      {
        "StreamId": "TPPrototype.uflsample.value_timeString",
        "DataType": "String",
        "Timestamp": "2013-12-01T06:00:00Z",
        "Value": "339.0"
      },
      {
        "StreamId": "TPPrototype.uflsample.value_timeString",
        "DataType": "String",
        "Timestamp": "2013-12-01T07:00:00Z",
        "Value": "344.0"
      },
      {
        "StreamId": "TPPrototype.uflsample.value_timeString",
        "DataType": "String",
        "Timestamp": "2013-12-01T17:00:00Z",
        "Value": "341.0"
      }
    ],
    "TPPrototype.uflsample.pressure_time": [
      {
        "StreamId": "TPPrototype.uflsample.pressure_time",
        "DataType": "Double",
        "Timestamp": "2013-12-01T06:00:00Z",
        "Value": 339.0
      },
      {
        "StreamId": "TPPrototype.uflsample.pressure_time",
        "DataType": "Double",
        "Timestamp": "2013-12-01T07:00:00Z",
        "Value": 344.0
      },
      {
        "StreamId": "TPPrototype.uflsample.pressure_time",
        "DataType": "Double",
        "Timestamp": "2013-12-01T17:00:00Z",
        "Value": 341.0
      }
    ]
  }
}
```

### CSV - Simple CSV column index example

```csv
2020-08-10T12:10:46.0928791Z,1.234567890
2020-08-10T12:10:47.0928791Z,12.34567890
2020-08-10T12:10:48.0928791Z,123.4567890
2020-08-10T12:10:49.0928791Z,1234.567890
2020-08-10T12:10:50.0928791Z,12345.67890
2020-08-10T12:10:51.0928791Z,123456.7890
2020-08-10T12:10:52.0928791Z,12345678.90
2020-08-10T12:10:53.0928791Z,123456789.0
```

### CSV - Simple CSV column header example

```csv
Date,Value
2020-08-10T12:10:46.0928791Z,1.234567890
2020-08-10T12:10:47.0928791Z,12.34567890
2020-08-10T12:10:48.0928791Z,123.4567890
2020-08-10T12:10:49.0928791Z,1234.567890
2020-08-10T12:10:50.0928791Z,12345.67890
2020-08-10T12:10:51.0928791Z,123456.7890
2020-08-10T12:10:52.0928791Z,12345678.90
2020-08-10T12:10:53.0928791Z,123456789.0
```

## Error handling
