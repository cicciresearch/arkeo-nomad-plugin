Each upload will be accompanied by a metadata file containing the device's information

```json
{
  "comment": "Upload contains perovskite solar cell JV measurements (raw data + NOMAD archive entries) with device stack metadata.",
  "datasets": [
    "PSC_JV_2026_Batch01"
  ],
  "entries": {
    "PSC_2026_001/JV_light_reverse.archive.json": {
      "comment": "Light JV (AM1.5G), reverse scan. Device structure included in entry metadata."
    }
  },
  "metadata": {
    "schema_hint": "custom_pv_jv",
    "device_family": "perovskite_solar_cell",
    "default_area_cm2": 0.050,
    "default_illumination": "AM1.5G",
    "device_structure_summary": "Glass/ITO/SAM/Perovskite/C60/BCP/Cu (example stack)"
  }
}
```

The full scan is converted to the NOMAD json structure to be properly uploaded

```json
{
  "archive": {
    "metadata": {
      "entry_name": "PSC_2026_001 | JV light reverse",
      "description": "Single JV scan of a perovskite solar cell under AM1.5G illumination.",
      "keywords": [
        "perovskite",
        "solar cell",
        "JV",
        "AM1.5G"
      ]
    },
    "results": {
      "properties": {
        "photovoltaics": {
          "active_area": {
            "value": 0.050,
            "unit": "cm^2"
          },
          "jsc": {
            "value": 22.10,
            "unit": "mA/cm^2"
          },
          "voc": {
            "value": 1.09,
            "unit": "V"
          },
          "ff": {
            "value": 0.78,
            "unit": "1"
          },
          "pce": {
            "value": 18.80,
            "unit": "%"
          }
        }
      }
    },
    "data": {
      "measurement_type": "JV",
      "sample": {
        "sample_id": "PSC_2026_001",
        "device_architecture": "p-i-n",
        "pixel_id": "A1",
        "masked_area": {
          "value": 0.050,
          "unit": "cm^2"
        }
      },
      "conditions": {
        "illumination": "AM1.5G",
        "irradiance": {
          "value": 100.0,
          "unit": "mW/cm^2"
        },
        "temperature": {
          "value": 25.0,
          "unit": "C"
        },
        "atmosphere": "N2",
        "relative_humidity": {
          "value": 0.1,
          "unit": "%"
        }
      },
      "protocol": {
        "scan_direction": "forward",
        "voltage_start": {
          "value": 1.20,
          "unit": "V"
        },
        "voltage_end": {
          "value": -0.20,
          "unit": "V"
        },
        "scan_rate": {
          "value": 0.10,
          "unit": "V/s"
        },
        "settling_time": {
          "value": 0.01,
          "unit": "s"
        },
        "prebias": {
          "value": 1.20,
          "unit": "V"
        },
        "prebias_time": {
          "value": 5.0,
          "unit": "s"
        }
      },
      "instrument": {
        "smu": "Arkeo SMU",
        "wiring": "4-wire",
        "current_compliance": {
          "value": 0.10,
          "unit": "A"
        }
      },
      "columns": [
        { "name": "time", "unit": "s" },
        { "name": "voltage", "unit": "V" },
        { "name": "current", "unit": "A" },
        { "name": "current_density", "unit": "mA/cm^2" }
      ],
      "points": [
        { "time": 0.000, "voltage": 1.200, "current": -0.001105, "current_density": -22.10 },
        { "time": 0.010, "voltage": 1.190, "current": -0.001095, "current_density": -21.90 },
        { "time": 0.020, "voltage": 1.180, "current": -0.001080, "current_density": -21.60 },
        { "time": 0.030, "voltage": 1.170, "current": -0.001060, "current_density": -21.20 },
        { "time": 0.040, "voltage": 1.160, "current": -0.001030, "current_density": -20.60 }
      ]
    }
  }
}

```