---
uid: JSONPathSyntaxForValueRetrieval
---

# JSONPath syntax for value retrieval

For information on which semantic is used for retrieving values from JSON files, see [JSONPath - XPath for JSON](https://goessner.net/articles/JsonPath/).

The following syntax is used to extract values from JSON documents.

## JSON - Simple JSONPath example

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

The following JSONPath configuration reads a series of values:

```json
{
    "Id": "DoubleValue",
    "FieldDefinition": "value",
    "DataType": "Double"
},
{
    "Id": "Timestamp",
    "FieldDefinition": "time",
    "DataType": "DateTime",
    "IsIndex": true
}
```

## Error handling

If you encounter Text Parser related errors that is errors for the **ValueField** or **TimeField**, check the StreamId associated with the error message.

Possible errors include the following:

- The JSONPath expression of **ValueField** or **TimeField** is pointing to a non-existing value
- The JSONPath expression of **ValueField** or **TimeField** is missing a value altogether
- **DataType** does not match the value