# MyCoast King Tide Flooding Data Source Codebook

**Date:** April 2, 2026
**Version:** 1.0
**Citation:** Penn Libraries Data Management Documentation Standards

---

## 1. Dataset Overview

**Dataset Title:** MyCoast: Rhode Island – Citizen-Reported King Tide Observations
**Source File:** `MyCoast_export_2026-03-26__1_.csv`
**Source Portal:** [https://mycoast.org/ri](https://mycoast.org/ri)
**Geographic Scope:** Providence, Providence County, Rhode Island, USA
**Records:** 153 rows | 27 columns
**Time Range:** Photo dates: 2008-12-12 to 2025-12-06; Records created: 2015-08-28 to 2025-12-06
**Data Type:** Crowdsourced observational data (photos + automated metadata)
**Primary Flood Source Category:** Coastal tidal flooding – King Tide events

### Description
Developed by the **University of Rhode Island (URI) Coastal Resources Center (CRC)** and **Rhode Island Sea Grant**, this platform allows the public to submit georeferenced photographs of flooding and coastal change. The system automatically appends contextual metadata — including tidal height from nearby NOAA gauges and local weather conditions — to each report. This export contains only **King Tide module** submissions from Providence, RI.

### Reporting Module Captured in This Export
1. **King Tides:** Documents extreme high tidal events through public photo submissions.

Other MyCoast modules (Storm Report, CoastSnap) are not included in this export.

---

## 2. Source & Access Information

* **Data Producer:** URI Coastal Resources Center / Rhode Island Sea Grant
* **Platform Partners:** RI Coastal Resources Management Council (CRMC), RI Department of Transportation (RIDOT), Save the Bay, and Woonasquatucket River Watershed Council (WRWC)
* **Funding:** Originally via NOAA/Northeast Ocean Council; $200,000 appropriated by RI in FY2026 for continued operations
* **Access Method:** Public web portal, mobile apps (iOS/Android), and a searchable database
* **Data License:** Reports are publicly visible; contact URI Sea Grant for large-scale downloads
* **Citation Format:** MyCoast: Rhode Island [dataset]. University of Rhode Island Coastal Resources Center / Rhode Island Sea Grant. [https://mycoast.org/ri](https://mycoast.org/ri)

---

## 3. Variable Descriptions

All coordinates are in **decimal degrees (WGS84)** and dates/times follow **ISO 8601** standards. Weather and tide metadata are automatically retrieved from external APIs at the time of report submission.

### 3.1 Report Identification

| Variable Name | Variable Label | Type | Values / Range | Missing Codes | Notes |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **ID #** | Report Identifier | Integer | Unique numeric ID (e.g., 227672) | None | Primary key; no missing values |
| **reportType** | Type of Report | Categorical | `King Tide` (all 153 records) | None | Export filtered to King Tide reports only |
| **report_icon** | Map Display Icon | Categorical | `tide.svg` (152), `nuisance.svg` (1) | None | Icon file used for map rendering on the MyCoast platform |
| **URL** | Report Permalink | String (URL) | `https://mycoast.org/reports/{ID}` | None | Public link to the report; no missing values |
| **embed** | Embed Flag/ID | Float | All null in this dataset | Blank | Can be dropped for all analyses |

### 3.2 Submission Metadata

| Variable Name | Variable Label | Type | Values / Range | Missing Codes | Notes |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **photo_date** | Date of Photo | Date (YYYY-MM-DD) | 2008-12-12 to 2025-12-06 | None | From submitter or device EXIF; pre-2015 dates may be backdated |
| **photo_time** | Time of Photo | String (H:MM am/pm) | 12-hour format (e.g., `8:37 am`) | None | Sourced from submitter or device |
| **report_created** | System Submission Timestamp | DateTime (ISO 8601, UTC) | 2015-08-28T12:41:24Z to 2025-12-06T13:47:34Z | None | When report was recorded by MyCoast; may differ from `photo_date` |
| **from_device** | Submission Device OS | Categorical | iOS or Android + version (e.g., `iOS 14.8`) | Blank (19 records, 12%) | Reflects OS version at submission time, not device model |
| **AuthorName** | Submitter Name | String | Redacted | Blank (all 153 records) | Fully redacted for privacy; drop for analysis |
| **AuthorEmail** | Submitter Email | String | Redacted | Blank (all 153 records) | Fully redacted for privacy; drop for analysis |

### 3.3 Media

| Variable Name | Variable Label | Type | Values / Range | Missing Codes | Notes |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **images** | Photo URL(s) | String (pipe-delimited URLs) | 1–5 URLs per report (min 1, max 5, median 1, mean ~1.75) | Blank (3 records) | Hosted on DigitalOcean Spaces; multiple URLs separated by `\|` |

### 3.4 Location

| Variable Name | Variable Label | Type | Values / Range | Missing Codes | Notes |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **location_longitude** | Longitude (WGS84) | Continuous | ~−71.4° (Providence, RI area) | -999 | Decimal degrees; no missing values in this export |
| **location_latitude** | Latitude (WGS84) | Continuous | ~41.8° (Providence, RI area) | -999 | Decimal degrees; no missing values in this export |
| **geo_administrative_area_level_1** | State | Categorical | `RI` (all records) | None | Derived from reverse geocoding (Google Maps API) |
| **geo_administrative_area_level_2** | County | Categorical | `Providence County` (all records) | None | Derived from reverse geocoding |
| **geo_locality** | City / Town | Categorical | `Providence` (all records) | None | Derived from reverse geocoding |
| **geo_neighborhood** | Neighborhood | String | Named neighborhood (e.g., `Downtown Providence`) | Blank (7 records) | Not all coordinates resolve to a named neighborhood |
| **geo_route** | Street Name / Route | String | Street name (e.g., `Exchange St`) | Blank (15 records) | Not all coordinates resolve to a named street |

### 3.5 Weather Conditions at Time of Submission

Weather data are automatically retrieved from a weather API at submission time, based on the report's coordinates and timestamp.

| Variable Name | Variable Label | Type | Values / Range | Missing Codes | Notes |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **weather_temperature** | Air Temperature (°F) | Continuous | 29.7 – 86.0 °F (mean: 58.2, median: 58.6) | None | Auto-fetched at submission time |
| **weather_windSpeed** | Wind Speed (mph) | Continuous | 0.0 – 18.3 mph (mean: 6.9, median: 7.3) | None | Auto-fetched at submission time |
| **weather_windBearing** | Wind Direction (°) | Integer | 0 – 360° (meteorological convention: direction wind comes *from*; 0/360=N, 90=E, 180=S, 270=W) | None | Auto-fetched at submission time |
| **weather_calc_24hr_precip** | 24-Hr Precipitation (in) | Continuous | 0.000 – 3.791 in (median: 0.000) | None | Total precipitation in 24 hrs preceding submission; most reports show 0 |

### 3.6 Tide Data

Tide data URLs are automatically appended at submission time based on the nearest NOAA tidal gauge. The station ID and date parameters embedded in these URLs can be parsed programmatically to extract gauge ID and observation window.

| Variable Name | Variable Label | Type | Values / Range | Missing Codes | Notes |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **TideDataObserved** | Observed Tide Data URL | String (URL) | NOAA Tides & Currents URL (datum: MLLW, units: feet) | None | Station ID embedded in URL (e.g., `8454000` = Providence, RI); all 153 records have a value |
| **TideDataPredicted** | Predicted Tide Data URL | String (URL) | NOAA tidal predictions URL for same gauge and date window | None | Pair with `TideDataObserved`; all 153 records have a value |

### 3.7 Narrative Content

| Variable Name | Variable Label | Type | Values / Range | Missing Codes | Notes |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **post_comment** | Submitter Comment | String (free text) | Written description of flooding observations | Blank (103 records, 67%) | Only 50 records (33%) include a comment |
| **MyCoastAI-description** | AI-Generated Photo Description | String (free text) | Automated description of submitted photo(s) | Blank (134 records, 88%) | Feature not widely deployed across this dataset's time range; use with caution |

---

## 4. Missing Data Codes

| Code | Label | Applies To |
| :--- | :--- | :--- |
| **Blank** | Not provided / Not applicable | `AuthorName`, `AuthorEmail`, `embed`, `from_device`, `geo_neighborhood`, `geo_route`, `post_comment`, `MyCoastAI-description`, `images` |
| **-999** | Not recorded (coordinates) | `location_latitude`, `location_longitude` |
| **None** | No missing values in this export | All other variables as noted above |

* `AuthorName` and `AuthorEmail` are fully redacted across all 153 records and can be dropped for all analyses.
* The `embed` column is entirely null and can be dropped.
* `post_comment` is absent in 67% of records; treat as sparse supplementary text.
* `MyCoastAI-description` is null in 88% of records; this AI feature was not widely deployed across the dataset's time range.

---

## 5. Data Notes & Limitations

* **Volunteer Accuracy:** Data quality depends on the submitter and should be treated as observational, not metrological. Reports should be validated against other sources before use in predictive models.
* **Geographic Scope:** This export is geographically uniform — all 153 records are from Providence, Providence County, RI. Geo-level fields and the tide station are therefore consistent across all records.
* **Temporal Note:** `photo_date` reflects when the photo was taken (EXIF or user input); `report_created` reflects when it was submitted to MyCoast. These differ for some records — use the appropriate field depending on your analysis.
* **Backdated Records:** Pre-2015 `photo_date` values (earliest: 2008-12-12) reflect photos submitted after the platform launched in 2015, with device EXIF dates preserved.
* **Tide URLs as Data:** The NOAA station ID and date parameters embedded in `TideDataObserved` / `TideDataPredicted` URLs can be parsed programmatically (e.g., station `8454000` = Providence, RI).
* **Metadata Auto-Fetch Mismatch:** Weather and tide metadata are fetched at submission time based on coordinates; mismatches may occur if a photo was taken at a different time or place than when/where it was submitted.
* **King Tide Module Only:** CoastSnap and Storm Report records are excluded from this export. Do not assume this dataset represents all MyCoast RI flooding observations.

---

## 6. Relationship to Other RI Flood Tools

MyCoast RI King Tide data complements two other URI-developed tools:

* **STORMTOOLS:** Provides modeled flood predictions. MyCoast King Tide photos serve as "ground truth" to validate these models at extreme high tide conditions.
* **RI-CHAMP:** A decision-support tool for infrastructure damage. King Tide observations can help validate CHAMP scenarios for nuisance and chronic tidal flooding.
* **NOAA Tidal Gauges (Station 8454000 – Providence):** All tide data URLs in this export reference this station. Observed and predicted tide data can be fetched directly from NOAA Tides and Currents using the embedded URLs.

Note: Unlike the MyCoast Storm Report export (which spans all RI counties and report types), this King Tide export is scoped to Providence only. Cross-referencing with the Storm Report dataset may provide complementary coverage for broader RI coastal flood analysis.

---

## 7. Documentation Reference

Prepared following the **Penn Libraries Data Management Resources** for Codebooks & Data Dictionaries.
* **Standards Used:** ISO 8601 for dates/times; enumerated missing data codes; versioned for reproducibility.
