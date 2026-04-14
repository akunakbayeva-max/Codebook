# VECINA Class – MyCoast Data Codebook

**Date:** April 13, 2026
**Version:** 1.0
**Citation:** Penn Libraries Data Management Documentation Standards

---

## 1. Dataset Overview

**Dataset Title:** VECINA Class – MyCoast Tagging Data

**Source Portal:** [VECINA MyCoast Data](https://docs.google.com/spreadsheets/d/161xvt7_7bJ78qqmoTLTctxBfIgdyCqOEI4vCefoD4-o/edit?usp=drive_link)

**Geographic Scope:** Rhode Island, USA (coastal and riverine communities)

**Time:** 2006-03-30 to 2026-01-25

**Data Type:** Crowdsourced observational data with manual class annotations

**Primary Flood Source Category:** Coastal tidal flooding, storm surge, king tides, and river flooding

### Description
This workbook contains MyCoast citizen-submitted flood reports tagged by VECINA class students. Each report consists of a georeferenced photo and associated metadata pulled from the MyCoast platform. Students independently annotated each photo with binary labels for scene content (ocean, river, street) and flood indicators (flooding, elevated water, damage). The dataset is structured for inter-rater reliability analysis, with two independent annotators assigned to each report.

### Sheets
1. **MyCoast Tagging:** Primary working sheet; student annotations plus MyCoast export fields.
2. **Assignments:** Tracks annotator assignments per report.
3. **MyCoast export 2026-02-07:** Full raw export from the MyCoast platform.

---

## 2. Source & Access Information

* **Data Producer:** URI Coastal Resources Center / Rhode Island Sea Grant (original MyCoast data); VECINA class annotators (tagging layer)
* **Platform Partners:** RI Coastal Resources Management Council (CRMC), RI Department of Transportation (RIDOT), Save the Bay, and Woonasquatucket River Watershed Council (WRWC)
* **Access Method:** Google Sheets (class access); MyCoast public portal at [https://mycoast.org/ri](https://mycoast.org/ri)
* **Data License:** MyCoast reports are publicly visible; annotations are class-produced
* **Citation Format:** VECINA Class MyCoast Tagging Data [dataset]. Bates College VECINA Program / URI Coastal Resources Center.

---

## 3. Variable Descriptions

All coordinates are in **decimal degrees (WGS84)** and dates/times follow **ISO 8601** standards.

### 3.1 MyCoast Export Fields (Cols 1–22)

These fields are pulled directly from the MyCoast platform export. See Section 3.3 for the full export schema.

| Variable Name | Variable Label | Type | Values / Range | Missing Codes | Notes |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **ID #** | Report Identifier | Integer | Unique numeric ID | None | Primary key |
| **reportType** | Type of Report | Categorical | King Tide (259), Storm Reporter (148), Coastal Resilience (3) | None | |
| **photo_date** | Date of Photo | Date (YYYY-MM-DD) | 2006-03-30 to 2026-01-25 | None | From device EXIF or user input |
| **photo_time** | Time of Photo | String | 12-hour format (e.g., `8:37 am`) | None | |
| **from_device** | Submission Device OS | Categorical | iOS or Android + version | Blank | |
| **URL** | Report Permalink | String (URL) | `https://mycoast.org/reports/{ID}` | None | |
| **images** | Photo URL(s) | String (pipe-delimited URLs) | 1+ URLs per report | Blank | Multiple URLs separated by `\|` |
| **location_longitude** | Longitude (WGS84) | Continuous | Decimal degrees | -999 | No missing values in this export |
| **location_latitude** | Latitude (WGS84) | Continuous | Decimal degrees | -999 | No missing values in this export |
| **geo_administrative_area_level_1** | State | Categorical | State abbreviation | None | From reverse geocoding |
| **geo_administrative_area_level_2** | County | String | County name | None | From reverse geocoding |
| **geo_locality** | City / Town | String | City or town name | None | From reverse geocoding |
| **geo_neighborhood** | Neighborhood | String | Named neighborhood | Blank | Not always resolvable |
| **geo_route** | Street Name | String | Street name | Blank | Not always resolvable |
| **weather_temperature** | Air Temperature (°F) | Continuous | Numeric | None | Auto-fetched at submission time |
| **weather_windSpeed** | Wind Speed (mph) | Continuous | Numeric | None | Auto-fetched at submission time |
| **weather_windBearing** | Wind Direction (°) | Integer | 0–360° (meteorological) | None | Direction wind comes *from* |
| **weather_calc_24hr_precip** | 24-Hr Precipitation (in) | Continuous | Numeric | None | Preceding 24 hours |
| **TideDataObserved** | Observed Tide Data URL | String (URL) | NOAA Tides & Currents URL | None | Datum: MLLW; units: feet |
| **TideDataPredicted** | Predicted Tide Data URL | String (URL) | NOAA tidal predictions URL | None | Same gauge and date window as observed |
| **MyCoastAI-description** | AI-Generated Photo Description | String (free text) | Automated description | Blank | Sparse; not widely deployed |
| **report_created** | Submission Timestamp | DateTime (ISO 8601, UTC) | UTC datetime | None | May differ from `photo_date` |

### 3.2 Annotation Fields (Cols 23–38)

Each report was independently tagged by two annotators. Annotator 1 occupies columns 23–30; Annotator 2 occupies columns 31–38. Column names for Annotator 2 are appended `.1` when read programmatically (e.g., `Flooding? (Y/N).1`).

| Variable Name | Variable Label | Type | Values / Range | Missing Codes | Notes |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Training photo? (Y/N)** | Training Photo Flag | Categorical | `Y`, `N`, `N?`, `?` | Blank | Exclude from inter-rater analyses |
| **Ocean? (Y/N)** | Ocean Visible | Binary | `Y`, `N` | Blank | Open saltwater, bay, or connected estuary |
| **River? (Y/N)** | River Visible | Binary | `Y`, `N`, `n` | Blank | Treat lowercase `n` as `N` |
| **Street? (Y/N)** | Street Visible | Binary | `Y`, `N` | Blank | Road, street, or paved surface |
| **Flooding? (Y/N)** | Flooding Observed | Binary | `Y`, `N` | Blank | Standing water in normally dry areas |
| **Elevated/Flood Alert? (Y/N)** | Elevated Water / Flood Alert | Binary | `Y`, `N`, `y` | Blank | Treat lowercase `y` as `Y` (16 records in Annotator 2) |
| **Damage? (Y/N)** | Damage Observed | Binary | `Y`, `N` | Blank | Physical damage to infrastructure or environment; more missing than other tags |
| **Comments** | Annotator Notes | String (free text) | Free text | Blank | ~14% of records; flags ambiguous cases |

### 3.3 Full MyCoast Export Fields (Sheet 3)

Sheet 3 contains the complete raw export from the MyCoast platform (410 rows, 83 columns). The Tagging sheet omits `AuthorName`, `AuthorEmail`, `post_comment`, `report_icon`, and `embed` relative to this export.

#### Storm Damage & Response Fields
*(From Storm Reporter reports; most sparsely populated)*

| Variable Name | Variable Label | Non-null |
| :--- | :--- | :--- |
| **storm_damage** | Overall storm damage observed (Y/N) | 149 |
| **road_damage** | Road damage (Y/N) | 137 |
| **road_damage_detail** | Road impact severity | 5 |
| **marinas_damage** | Marina damage (Y/N) | 76 |
| **buildings_damage** | Building damage (Y/N) | 76 |
| **hazmat_damage** | Hazardous materials release (Y/N) | 5 |
| **beach_damage** | Beach damage (Y/N) | 76 |
| **structure_damage** | Damage to docks/seawalls (Y/N) | 76 |
| **natural_damage** | Natural/environmental damage (Y/N) | 137 |
| **response_damage** | Emergency response observed | 2 |

#### Flooding Detail Fields

| Variable Name | Variable Label | Non-null |
| :--- | :--- | :--- |
| **flooding_cause** | Cause of flooding | 26 |
| **flooding_what** | What was flooded | 12 |
| **est_water_depth** | Estimated water depth | 3 |

#### Coastal Resilience Fields
*(From Coastal Resilience reports; ~2–3 records only)*

| Variable Name | Variable Label | Non-null |
| :--- | :--- | :--- |
| **site_type** | Physical site type | 2 |
| **infrastructure** | Type of coastal infrastructure | 3 |
| **stability** | Shoreline stability | 2 |
| **vegetative_cover_amount** | Amount of vegetation | 2 |
| **dominant_vegetation** | Dominant plant type | 2 |

---

## 4. Missing Data Codes

| Code | Label | Applies To |
| :--- | :--- | :--- |
| **Blank** | Not provided / Not applicable | Annotation fields, free-text fields, redacted fields |
| **-999** | Not recorded (coordinates) | `location_latitude`, `location_longitude` |
| **None** | No missing values in this export | Core ID, URL, date, and tide fields |

---

## 5. Data Notes & Limitations

* **Inter-Rater Reliability:** The dataset is structured for IRR analysis. Training photos (flagged `Y` in `Training photo? (Y/N)`) should be excluded before computing agreement metrics.
* **Case Inconsistencies:** Annotators used lowercase (`y`, `n`) and uncertain entries (`Y?`, `N?`, `?`). Lowercase variants should be uppercased; uncertain responses should be handled with a defined protocol (e.g., treated as missing or coded separately).
* **Annotator 2 Lowercase `y`:** The `Elevated/Flood Alert?` column for Annotator 2 contains 16 lowercase `y` entries; treat as `Y`.
* **Unannotated Rows:** Approximately 35–43 rows per annotator are blank and not yet tagged.
* **Sparse Damage Field:** `Damage? (Y/N)` has more missing values than other annotation fields (~349 non-null vs. ~373 for other tags), suggesting some annotators skipped it more frequently.
* **Privacy:** `AuthorName`, `AuthorEmail`, and `embed` are entirely null — redacted in this export.
* **Temporal Note:** `photo_date` reflects when the photo was taken; `report_created` reflects submission time. Use the appropriate field depending on your analysis.

---

## 6. Relationship to Other RI Flood Tools

* **STORMTOOLS:** Provides modeled flood predictions. MyCoast photos serve as ground truth for model validation.
* **RI-CHAMP:** A decision-support tool for infrastructure damage. MyCoast `Damage?` annotations provide observational validation for CHAMP scenarios.
* **NOAA Tidal Gauges:** Tide data URLs in the export reference the nearest NOAA station. Observed and predicted data can be fetched directly from the embedded URLs.

---

## 7. Documentation Reference

Prepared following the **Penn Libraries Data Management Resources** for Codebooks & Data Dictionaries.
* **Standards Used:** ISO 8601 for dates/times; enumerated missing data codes; versioned for reproducibility.

