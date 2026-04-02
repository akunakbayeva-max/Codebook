# Codebook: MyCoast King Tide Report Export
**File:** `MyCoast_export_2026-03-26__1_.csv`  
**Records:** 153 rows  
**Columns:** 27  
**Coverage:** All records are King Tide reports from Providence, Providence County, Rhode Island.  
**Date range:** Photo dates from 2008-12-12 to 2025-12-06; records created in the system from 2015-08-28 to 2025-12-06.

---

## Report Identification

### `ID #`
- **Type:** Integer
- **Description:** Unique numeric identifier assigned by MyCoast to each submitted report.
- **Example:** `227672`
- **Notes:** No missing values.

### `reportType`
- **Type:** String (categorical)
- **Description:** Category of observation submitted.
- **Values in this dataset:** `King Tide` (all 153 records)
- **Notes:** This export was filtered to King Tide reports only.

### `report_icon`
- **Type:** String (categorical)
- **Description:** Icon file associated with the report type, used for map display on the MyCoast platform.
- **Values:** `tide.svg` (152), `nuisance.svg` (1)

### `URL`
- **Type:** String (URL)
- **Description:** Public permalink to the report on the MyCoast website.
- **Example:** `https://mycoast.org/reports/227672`
- **Notes:** No missing values.

### `embed`
- **Type:** Float
- **Description:** Appears to be an embed flag or ID. All 153 values are null in this dataset.

---

## Submission Metadata

### `photo_date`
- **Type:** String (date, format `YYYY-MM-DD`)
- **Description:** Date the photo was taken, as reported by the submitter or device.
- **Range:** 2008-12-12 to 2025-12-06
- **Notes:** No missing values. Earlier dates (pre-2015) may reflect backdated photo metadata from device EXIF data.

### `photo_time`
- **Type:** String (12-hour time, format `H:MM am/pm`)
- **Description:** Time the photo was taken, as reported by the submitter or device.
- **Example:** `8:37 am`
- **Notes:** No missing values.

### `report_created`
- **Type:** String (ISO 8601 datetime, UTC, format `YYYY-MM-DDTHH:MM:SSZ`)
- **Description:** Timestamp when the report was submitted to and recorded by the MyCoast system.
- **Range:** 2015-08-28T12:41:24Z to 2025-12-06T13:47:34Z
- **Notes:** Will differ from `photo_date`/`photo_time` if the photo was taken earlier and submitted later.

### `from_device`
- **Type:** String (categorical)
- **Description:** Operating system and version of the device used to submit the report.
- **Examples:** `iOS 14.8`, `Android 9`, `Android 5.1.1`
- **Missing:** 19 records (12%)
- **Notes:** Version strings reflect the OS version at time of submission, not device model.

### `AuthorName`
- **Type:** Float / String
- **Description:** Name of the submitting user.
- **Missing:** All 153 records — entirely redacted in this export, likely for privacy.

### `AuthorEmail`
- **Type:** Float / String
- **Description:** Email address of the submitting user.
- **Missing:** All 153 records — entirely redacted in this export, likely for privacy.

---

## Media

### `images`
- **Type:** String (pipe-delimited list of URLs)
- **Description:** One or more URLs pointing to photos attached to the report, hosted on DigitalOcean Spaces. Multiple image URLs are separated by `|`.
- **Example:** `https://report-images.nyc3.digitaloceanspaces.com/.../abc123.jpg|https://...def456.jpg`
- **Image count per report:** Min 1, max 5, median 1, mean ~1.75
- **Missing:** 3 records

---

## Location

### `location_longitude`
- **Type:** Float (decimal degrees)
- **Description:** Longitude coordinate of the report location (WGS 84).
- **Notes:** No missing values. All records fall in the Providence, RI area (approximately −71.4°).

### `location_latitude`
- **Type:** Float (decimal degrees)
- **Description:** Latitude coordinate of the report location (WGS 84).
- **Notes:** No missing values. All records fall in the Providence, RI area (approximately 41.8°).

### `geo_administrative_area_level_1`
- **Type:** String
- **Description:** State or top-level administrative area, derived from reverse geocoding the coordinates (Google Maps API levels).
- **Values in this dataset:** `RI` (all 153 records)

### `geo_administrative_area_level_2`
- **Type:** String
- **Description:** County or second-level administrative area from reverse geocoding.
- **Values in this dataset:** `Providence County` (all 153 records)

### `geo_locality`
- **Type:** String
- **Description:** City or town from reverse geocoding.
- **Values in this dataset:** `Providence` (all 153 records)

### `geo_neighborhood`
- **Type:** String
- **Description:** Neighborhood name from reverse geocoding, when available.
- **Example:** `Downtown Providence`
- **Missing:** 7 records — not all locations resolve to a named neighborhood.

### `geo_route`
- **Type:** String
- **Description:** Street name or route from reverse geocoding, when available.
- **Example:** `Exchange St`
- **Missing:** 15 records — not all locations resolve to a named street.

---

## Weather Conditions at Time of Submission

Weather data are automatically retrieved from a weather API at the time the report is submitted, based on the report's coordinates and timestamp.

### `weather_temperature`
- **Type:** Float
- **Unit:** Degrees Fahrenheit
- **Description:** Ambient air temperature at the report location and time.
- **Range:** 29.7 – 86.0 °F (mean: 58.2 °F, median: 58.6 °F)
- **Missing:** None

### `weather_windSpeed`
- **Type:** Float
- **Unit:** Miles per hour (mph)
- **Description:** Wind speed at the report location and time.
- **Range:** 0.0 – 18.3 mph (mean: 6.9 mph, median: 7.3 mph)
- **Missing:** None

### `weather_windBearing`
- **Type:** Integer
- **Unit:** Degrees (meteorological convention: direction wind is coming *from*, 0/360 = North, 90 = East, 180 = South, 270 = West)
- **Description:** Wind direction at the report location and time.
- **Range:** 0 – 360°
- **Missing:** None

### `weather_calc_24hr_precip`
- **Type:** Float
- **Unit:** Inches
- **Description:** Calculated total precipitation in the 24 hours preceding the report submission.
- **Range:** 0.000 – 3.791 inches (median: 0.000 — most reports recorded no precipitation)
- **Missing:** None

---

## Tide Data

Tide data URLs are automatically appended at submission time based on the nearest NOAA tidal gauge to the report location.

### `TideDataObserved`
- **Type:** String (URL)
- **Description:** URL to the NOAA Tides and Currents page showing observed water level data for the gauge nearest to the report, centered on the report date (±1 day window). Datum is MLLW (Mean Lower Low Water); units are standard (feet).
- **Example:** `https://tidesandcurrents.noaa.gov/waterlevels.html?id=8454000&...`
- **Notes:** All 153 records have a value. The station ID embedded in the URL (e.g., `8454000` = Providence, RI) can be used to identify the gauge.

### `TideDataPredicted`
- **Type:** String (URL)
- **Description:** URL to the NOAA tidal predictions page for the same gauge and date window, showing predicted high/low tide times and heights.
- **Example:** `https://tidesandcurrents.noaa.gov/noaatidepredictions.html?action=dailychart&id=8454000&...`
- **Notes:** All 153 records have a value.

---

## Narrative Content

### `post_comment`
- **Type:** String (free text)
- **Description:** Written comment or description provided by the submitter at the time of report.
- **Example:** `"Water coming up through the drainage grates and between the gap in the granite edging along the river in Waterplace Park"`
- **Non-null:** 50 records (33%); 103 records (67%) have no comment.

### `MyCoastAI-description`
- **Type:** String (free text)
- **Description:** Automated description of the submitted photo(s) generated by MyCoast's AI image analysis system.
- **Non-null:** 19 records (12%); 134 records (88%) are null, suggesting this feature was not yet widely deployed across this dataset's time range.

---

## Notes on the Dataset

- **Geographic scope:** This export is entirely within Providence, RI. The geo-level fields and tide station are therefore uniform across all records.
- **Privacy:** `AuthorName` and `AuthorEmail` are fully redacted; the `embed` column is entirely null. These columns can be dropped for most analyses.
- **Temporal note:** `photo_date` reflects when the photo was taken (from EXIF or user input); `report_created` reflects when it was submitted to MyCoast. For most records these are the same day, but not always.
- **Tide URLs as data:** The NOAA station ID and date parameters embedded in `TideDataObserved` / `TideDataPredicted` URLs can be parsed to extract the gauge ID and observation window programmatically.
