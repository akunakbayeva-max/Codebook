# MyCoast:MyCoast Flooding Data Source Codebook

**Date:** April 2, 2026  
**Version:** 1.0  
**Citation:** Penn Libraries Data Management Documentation Standards

--- 

## 1. Dataset Overview

**Dataset Title:** MyCoast: Rhode Island – Citizen-Reported Flooding Observations
**Source Portal:** [https://mycoast.org/ri](https://mycoast.org/ri) 
**Geographic Scope:** State of Rhode Island, USA (primary focus: Providence and coastal/riverine communities) 
**Time:** 2014 (platform launch) – present
**Data Type:** Crowdsourced observational data (photos + data) 
**Primary Flood Source Category:** Coastal tidal flooding, storm surge, king tides, and river flooding 

### Description
Developed by the **University of Rhode Island (URI) Coastal Resources Center (CRC)** and **Rhode Island Sea Grant**, this platform allows the public to submit georeferenced photographs of flooding and coastal change. The system automatically appends contextual metadata, such as tidal height from NOAA gauges and local weather data, to each report.

### Reporting Modules
1.  **King Tides:** Documents extreme high tidal events.
2.  **Storm Report:** Captures flooding and damage from coastal storms and nor'easters.
3.  **CoastSnap:** Records shoreline change from fixed camera stations.

---

## 2. Source & Access Information

* **Data Producer:** URI Coastal Resources Center / Rhode Island Sea Grant 
* **Platform Partners:** RI Coastal Resources Management Council (CRMC), RI Department of Transportation (RIDOT), Save the Bay, and Woonasquatucket River Watershed Council (WRWC)
* **Funding:** Originally via NOAA/Northeast Ocean Council; $200,000 appropriated by RI in FY2026 for continued operations 
* **Access Method:** Public web portal, mobile apps (iOS/Android), and a searchable database 
* **Data License:** Reports are publicly visible; contact URI Sea Grant for large-scale downloads
* **Citation Format:** MyCoast: Rhode Island [dataset]. University of Rhode Island Coastal Resources Center / Rhode Island Sea Grant. [https://mycoast.org/ri](https://mycoast.org/ri). 

---

## 3. Variable Descriptions

All coordinates are in **decimal degrees (WGS84)** and dates/times follow **ISO 8601** standards.

| Variable Name | Variable Label | Type | Values / Range | Missing Codes | Notes |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **report_id** | Report Identifier | String | Unique alphanumeric ID | -9 | Primary key  |
| **report_type** | Type of Report | Categorical | 1=King Tides, 2=Storm, 3=CoastSnap | -9 | Distinguishes report source  |
| **submission_date** | Date of Submission | Date | YYYY-MM-DD | -9 | Date submitted to platform |
| **observation_date**| Date of Observation | Date | YYYY-MM-DD | -9 | Sourced from photo EXIF  |
| **latitude** | Latitude (WGS84) | Continuous | ~41.1°N – 42.0°N | -999 | Auto-populated or manual  |
| **longitude** | Longitude (WGS84) | Continuous | ~-71.9°E – -71.1°E | -999 | ]Negative = West  |
| **city_town** | Municipality | String | RI municipality name | Blank | Derived from coordinates |
| **county** | County | Categorical | 1=Providence, 2=Washington, 3=Kent, 4=Newport, 5=Bristol | -9 | RI County  |
| **coastal_inland** | Coastal/Inland | Categorical | 1=Coastal, 2=Inland, 3=Both | -9 | Proximity to water source  |
| **tide_height_ft** | Tide Height (ft) | Continuous | Numeric (ft above MLLW) | -9 | Nearest NOAA station data  |
| **tide_type** | Tidal Classification| Categorical | 1=King Tide, 2=High, 3=Low, 4=Storm Surge, 5=Other | -9 | Thresholds set by RI Sea Grant  |
| **weather_condition**| Weather Condition | Categorical | 1=Clear, 2=Cloudy, 3=Rain, 4=Heavy Rain, 5=Snow, 6=Fog, 9=Other | -9 |Auto-fetched or reported  |
| **flooding_observed**| Flooding Observed | Binary | 1=Yes, 0=No | -9 |Presence of water in photo |
| **flood_severity** | Flood Severity | Ordinal | 1=Minor, 2=Moderate, 3=Severe, 4=Extreme, 9=Unknown | -9 | Qualitative estimate  |
| **infrastructure_affected** | Assets Affected | Categorical | 0=None, 1=Road, 2=Parking, 3=Resid., 4=Comm., 5=Park, 6=Utility, 7=Seawall, 8=Other | -9 | Multi-value possible |
| **stormtools_linked**| STORMTOOLS Linked | Binary | 1=Yes, 0=No | -9 |]Cross-validated with model  |

---

## 4. Missing Data Codes

| Code | Label | Applies To |
| :--- | :--- | :--- |
| **-9** | Not recorded / Not available | All numeric and categorical variables  |
| **-999** | Not recorded (coordinates) | Latitude and Longitude  |
| **Blank** | Not provided | String and free-text fields  |
| **0** | No / Not observed | Binary variables (e.g., flooding_observed)  |

---

## 5. Data Notes & Limitations

* **Volunteer Accuracy:** Data quality depends on the submitter and should be treated as observational, not metrological.
* **Metadata Retrieval:** Tidal and weather data are auto-fetched from the nearest station; mismatches may occur for inland reports.
* **Qualitative Severity:** The `flood_severity` field is an estimate, not a measured water depth.
* **CoastSnap:** These reports track shoreline change over time and should be flagged when used in flood-only datasets.
* **Inland Coverage:** Prior to 2022, reports are predominantly coastal; inland reporting has expanded recently.
---

## 6. Relationship to Other RI Flood Tools

MyCoast RI data complements two other URI-developed tools:

* **STORMTOOLS:** Provides modeled flood predictions. MyCoast photos serve as "ground truth" to validate these models].
* **RI-CHAMP:** A decision-support tool for infrastructure damage. MyCoast reports on `infrastructure_affected` provide validation for CHAMP scenarios.

---

## 7. Documentation Reference

Prepared following the **Penn Libraries Data Management Resources** for Codebooks & Data Dictionaries.
* **Standards Used:** ISO 8601 for dates/times; enumerated missing data codes; versioned for reproducibility.
