# /api/v0/data/

There is no `PUT` request handling, because data frames are read-only.

## POST

### Request Schema

**Headers:**
```json
"Authorization": "Key {deviceAPIKey}"
```

**JSON Body:**
```json
{
  "type": "object",
  "properties": {
    "deviceId": {
      "description": "The unique device ID string.",
      "type": "string"
      },
    "datetime": {
      "description": "An ISO 8601 formatted date/time string.",
      "type": "string",
      },
    "location": {
      "description": "A two-part floating point representation of the sensor's coordinates.",
      "type": "array",
      "items": {
        "type": "number"
        },
      "minItems": 2,
      },
    "data": {
      "description": "A sparsely populated data frame of sensor readings.",
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "target": {
            "description": "A string representing the condition reported by the sensor",
            "type": "string",
            "choices": ["SO2", "O3", "NO2", "CO", "H2S", "TEMP", "HUMID"]
            },
          "value": {
            "description": "A floating point representation of the sensor's reading.",
            "type": "number"
            },
          "unit": {
            "description": "A string representing the unit of measurement corresponding to value of the reading.",
            "type": "string",
            "choices": ["PPM", "GM3", "F", "C", "PCT"]
            },
          "sensor": {
            "description": "A string representing the type of sensor that took the reading (e.g. SPEC_NO2_20).",
            "type": "string"
            }
          },
        "required": ["target", "value", "unit", "sensor"]
        },
      "minItems": 1
      }
    }
  },
  "required": ["datetime", "location", "data"]
}
```

### Example Request

**Headers:**
```json
"Authorization": "Key vIrm6BabtJVRrVEZJJQAgFx4v74CuLkb"
```

**JSON Body:**
```json
{
  "datetime": "2017-07-16T19:20:30.45+01:00",
  "location": [-23.4423, 14.449],
  "data": [
    {
      "target": "TEMP",
      "value": 15.201,
      "unit": "C",
      "sensor": "TH02"
    },
    {
      "target": "SO2",
      "value": 23.125,
      "unit": "PPM",
      "sensor": "SPEC_SO2_100"
    },
    {
      "target": "O3",
      "value": 10.213,
      "unit": "PPM",
      "sensor": "SPEC_O3_20"
    },
    {
      "target": "CO",
      "value": 44.412,
      "unit": "PPM",
      "sensor": "SPEC_CO_1000"
    }
  ]
}
```

### Example Response

The API assumes all `POST` requests originate from devices in the field that don't need any followup information.

* Success: `204 NO CONTENT`
* Authentication Failure: `401 NOT AUTHORIZED`
* Failure: `400 BAD REQUEST`

## GET

Data defaults to open access. We can close this later if need be.

**Query Parameters:**
```json
{
  "type": "object",
  "properties": {
    "limit": {
      "description": "The maximum number of data points per request."
      "type": "number",
      "default": 100
      },
    "offset": {
      "description": "The number of data points to skip."
      "type": "number",
      "default": 0
    }
  }
  "required": []
}
```

## DELETE

Deleting a datapoint requires device-level authentication. An empty JSON body will delete nothing.

Future modifications may include the ability to delete specific sensor results.

### Request Schema

**Headers:**
```json
"Authorization": "Key {deviceAPIKey}"
```

**JSON Body:**
```json
{
  "type": "object",
  "parameters": {
    "datetime": {
      "description": "An ISO 8601 formatted date string (will delete any matching)."
      "type": "string"
      },
    "datetime_lt": {
      "description": "An ISO 8601 formatted date string (will delete all entries prior)."
      "type": "string"
    },
    "datetime_gt": {
      "description": "An ISO 8601 formatted date string (will delete all entries after)."
      "type": "string"
    }
  }
}
```

### Example Response

* Success: `204 NO CONTENT`
* Authentication Failure: `401 NOT AUTHORIZED`
* Failure: `400 BAD REQUEST`

