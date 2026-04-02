# NCEI Storm Events Database: Codebook

**Date:** April 2, 2026  
**Version:** 1.0  
**Citation:** Penn Libraries Data Management Documentation Standards

---

## 1. Dataset Overview

**Dataset Title:** Storm Events Database  
**Source Portal:** [National Centers for Environmental Information (NCEI)](https://www.ncdc.noaa.gov/stormevents/)  
**Geographic Scope:** United States (all states and territories)  
**Time:** 1950 – present  
**Data Type:** Meteorological observational and impact data  
**Primary Event Categories:** Tornadoes, Thunderstorms, Floods, Hail, Hurricanes, and extreme weather phenomena

### Description
The Storm Events Database is the official record of significant weather phenomena in the United States. It captures events with sufficient intensity to cause loss of life, injuries, or significant property damage, as well as rare meteorological events that generate significant media attention.

---

## 2. Source & Access Information

* **Data Producer:** NOAA National Centers for Environmental Information (NCEI)
* **Platform Partners:** National Weather Service (NWS)
* **Access Method:** Public web portal, searchable database, and bulk CSV downloads
* **Data License:** Public domain; citation requested
* **Citation Format:** Storm Events Database - Search Results. National Centers for Environmental Information. [https://www.ncdc.noaa.gov/stormevents/](https://www.ncdc.noaa.gov/stormevents/).

---

## 3. Variable Descriptions

All dates/times follow **ISO 8601** standards where applicable.

| Variable Name | Variable Label | Type | Values / Range | Missing Codes | Notes |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **event_id** | Event Identifier | String | Unique alphanumeric ID | -9 | Primary key |
| **episode_id** | Episode Identifier | String | Unique alphanumeric ID | -9 | Links related events |
| **state** | State | String | U.S. State/Territory | Blank | Full name of state |
| **event_type** | Type of Event | Categorical | ~48 official types | -9 | e.g., Tornado, Hail |
| **begin_date_time**| Start Time | Date/Time | YYYY-MM-DD HH:MM | -9 | Local time of onset |
| **end_date_time** | End Time | Date/Time | YYYY-MM-DD HH:MM | -9 | Local time of end |
| **injuries_direct** | Direct Injuries | Continuous | Integer (0+) | -9 | Attributed to event |
| **deaths_direct** | Direct Deaths | Continuous | Integer (0+) | -9 | Attributed to event |
| **damage_property**| Property Damage | String | Numeric + (K/M/B) | Blank | Estimated USD |
| **damage_crops** | Crop Damage | String | Numeric + (K/M/B) | Blank | Estimated USD |
| **magnitude** | Event Magnitude | Continuous | Numeric | -9 | Wind speed/Hail size |
| **source** | Data Source | Categorical | Law Enf, Public, NWS | -9 | Who reported the event |

---

## 4. Missing Data Codes

| Code | Label | Applies To |
| :--- | :--- | :--- |
| **-9** | Not recorded / Not available | All numeric and categorical variables |
| **Blank** | Not provided | String and free-text fields |
| **0** | No / Not observed | Binary or count variables (e.g., deaths) |

---

## 5. Data Notes & Limitations

* **Reporting Thresholds:** Significant events are recorded based on damage, fatalities, or rarity; minor events may be excluded.
* **Estimate Accuracy:** Damage figures are estimates and may vary in precision depending on the reporting source.
* **Historical Variability:** Data from 1950–1995 primarily focused on tornadoes, thunderstorm winds, and hail; full coverage of all 48 event types began in 1996.
* **Update Lag:** Data typically appears in the database with a 120-day delay to allow for NWS verification.

---

## 6. Relationship to Other Tools

* **NWS Storm Data Publication:** Provides a narrative summary that accompanies the database entries.
* **Hazards U.S. (HAZUS):** FEMA-based models that often utilize NCEI historic data for risk assessment.

---

## 7. Documentation Reference

Prepared following the **Penn Libraries Data Management Resources** for Codebooks & Data Dictionaries.
* **Standards Used:** ISO 8601 for dates/times; enumerated missing data codes; versioned for reproducibility.
