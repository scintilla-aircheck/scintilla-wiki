# /api/v0/data/

## POST

### Schema

**Headers:**
```json
"Authorization": "Key {deviceAPIKey}"
```

**JSON Body:**
```json
{
  "type": "object",
  "properties": {
    "datetime": {
      "description": "An ISO 8601 formatted date/time string",
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
    },
    {
      "target": "NO2",
      "value": 5.112,
      "unit": "PPM",
      "sensor": "SPEC_NO2_20"
    },
    {
      "target": "H2S",
      "value": 5.199,
      "unit": "PPM",
      "sensor": "SPEC_H2S_50"
    },
    {
      "target": "PM2_5",
      "value": 0.334,
      "unit": "GM3",
      "sensor": "SDS021"
    },
    {
      "target": "PM10",
      "value": 0.734,
      "unit": "GM3",
      "sensor": "SDS021"
    }
  ]
}
```

## GET

## PUT

## DELETE
