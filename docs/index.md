# ARKEO → NOMAD Integration

<figure markdown="span">
  ![fixture](assets/images/Untitled.jpg){ .on-glb width="60%"}
  <figcaption></figcaption>
</figure>

## Overview

The **NOMAD (Novel Materials Discovery) platform** is a European research data infrastructure designed to store, share, and analyze materials science data in a FAIR-compliant way (Findable, Accessible, Interoperable, Reusable). It supports both computational and experimental datasets, including photovoltaic and perovskite research.

Integrating ARKEO with NOMAD allows users to:

* Store measurement data in a structured and standardized format
* Ensure reproducibility of experiments
* Share datasets with collaborators or the public
* Automatically generate persistent identifiers (DOIs)

ARKEO provides a streamlined workflow to export measurement data and metadata into a NOMAD-compatible format, enabling direct upload to the NOMAD repository or automated ingestion through custom parsers.

---

## ARKEO Integration Concept

ARKEO generates measurement files (e.g., JV scans, MPPT stability tests) in ASCII format. These files include measurement metadata and are converted into structured JSON objects compatible with NOMAD’s data model.

The integration workflow is as follows:

1. **Measurement Execution**
   Data is acquired using ARKEO routines (JV, MPPT, etc.).

2. **Metadata Enrichment (Optional)**
   Users may add device information such as architecture, layer stack, and composition.

3. **Export to NOMAD Format**
   ARKEO converts raw data into a structured JSON format.

4. **Upload to NOMAD**
   Data can be uploaded manually or via API integration.

---

## Data Structure

Each experiment is represented as a single JSON object containing:

* Sample information
* Instrument details
* Environmental conditions
* Illumination settings
* One or more measurements

### General Structure

```json
{
  "entry_type": "experiment",
  "sample": { ... },
  "instrument": { ... },
  "environment": { ... },
  "illumination": { ... },
  "measurements": [ ... ]
}
```

---

## Sample Information

```json
{
  "sample": {
    "name": "Device_001",
    "area": { "value": 0.1, "unit": "cm^2" },
    "architecture": "n-i-p",
    "layer_stack": ["Glass", "ITO", "SnO2", "Perovskite", "Spiro", "Au"],
    "composition": "FA0.85MA0.15PbI3",
    "encapsulation": true
  }
}
```

---

## Instrument Information

```json
{
  "instrument": {
    "name": "ARKEO Multichannel",
    "manufacturer": "Cicci Research",
    "software_version": "x.x.x",
    "channel_id": 1
  }
}
```

---

## Environment

```json
{
  "environment": {
    "temperature": { "value": 25, "unit": "C" },
    "humidity": { "value": 40, "unit": "%" },
    "atmosphere": "air"
  }
}
```

---

## Illumination

```json
{
  "illumination": {
    "type": "AM1.5G",
    "source": "Solar simulator",
    "intensity": { "value": 100, "unit": "mW/cm^2" },
    "calibration": "reference cell"
  }
}
```

---

## JV Measurement Example

```json
{
  "type": "JV",
  "timestamp": "2026-04-15T10:30:00Z",
  "parameters": {
    "scan_direction": "forward",
    "scan_rate": { "value": 0.1, "unit": "V/s" }
  },
  "data": {
    "voltage": { "values": [0.0, 0.1, 0.2], "unit": "V" },
    "current_density": { "values": [0.0, 1.2, 2.3], "unit": "mA/cm^2" }
  },
  "results": {
    "Voc": { "value": 1.1, "unit": "V" },
    "Jsc": { "value": 22, "unit": "mA/cm^2" },
    "FF": { "value": 0.78 },
    "efficiency": { "value": 18.9, "unit": "%" }
  }
}
```

---

## Stability (MPPT) Example

```json
{
  "type": "stability",
  "subtype": "MPPT",
  "timestamp": "2026-04-15T11:00:00Z",
  "parameters": {
    "tracking_algorithm": "perturb_and_observe",
    "sampling_interval": { "value": 1, "unit": "s" }
  },
  "data": {
    "time": { "values": [0, 1, 2], "unit": "s" },
    "voltage": { "values": [0.9, 0.91, 0.92], "unit": "V" },
    "current": { "values": [0.02, 0.021, 0.021], "unit": "A" }
  }
}
```

---

## Notes and Best Practices

* Always include units for all quantities
* Provide device area for correct normalization
* Include time axis for stability measurements
* Add metadata progressively if not available during acquisition

---

## Summary

The ARKEO–NOMAD integration enables seamless transition from measurement to FAIR data publication. By exporting structured JSON datasets and optionally using a NOMAD parser, ARKEO ensures that experimental data is immediately usable within modern research data infrastructures.
