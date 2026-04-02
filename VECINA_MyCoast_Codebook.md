# Codebook: VECINA Class – MyCoast Data
**File:**[VECINA MyCoast Data](https://docs.google.com/spreadsheets/d/161xvt7_7bJ78qqmoTLTctxBfIgdyCqOEI4vCefoD4-o/edit?usp=drive_link) 
**Sheets:** 3 — `MyCoast Tagging`, `Assignments`, `MyCoast export 2026-02-07`

---

## Sheet 1: `MyCoast Tagging`

**Purpose:** The primary working sheet for the class. Students manually tag each MyCoast report photo with a set of binary yes/no labels. Each row is one report; columns 1–22 are data pulled from the MyCoast export, and columns 23–38 contain the annotation fields filled in by two independent annotators.

**Rows:** 410 data rows (header spans rows 1–2: row 1 has group labels "Data submitted through app" and "Damage? (Y/N)" / "Annotator 2"; row 1 contains the actual column names.)

### Header Structure
The sheet uses a two-row header:
- **Row 1:** Section labels — `Data submitted through app` (cols 1–22), `Damage? (Y/N)` (cols 23–30, Annotator 1), `Annotator 2` (cols 31–38)
- **Row 2:** Column names used throughout this codebook

---

### MyCoast Data Columns (Cols 1–22)
These are pulled directly from the MyCoast export. See **Sheet 3** for full definitions. The tagging sheet omits `AuthorName`, `AuthorEmail`, `post_comment`, `report_icon`, and `embed` relative to the full export.

| Column | Description |
|---|---|
| `ID #` | Unique MyCoast report ID |
| `reportType` | Report category (King Tide, Storm Reporter, Coastal Resilience) |
| `photo_date` | Date photo was taken |
| `photo_time` | Time photo was taken |
| `from_device` | Submitter's OS and version |
| `URL` | Link to report on mycoast.org |
| `images` | Pipe-delimited image URL(s) |
| `location_longitude` | Decimal degrees longitude (WGS 84) |
| `location_latitude` | Decimal degrees latitude (WGS 84) |
| `geo_administrative_area_level_1` | State |
| `geo_administrative_area_level_2` | County |
| `geo_locality` | City/town |
| `geo_neighborhood` | Neighborhood (sometimes null) |
| `geo_route` | Street name (sometimes null) |
| `weather_temperature` | Air temp at submission (°F) |
| `weather_windSpeed` | Wind speed at submission (mph) |
| `weather_windBearing` | Wind direction (degrees, meteorological) |
| `weather_calc_24hr_precip` | 24-hr precipitation prior to submission (inches) |
| `TideDataObserved` | URL to NOAA observed water level data |
| `TideDataPredicted` | URL to NOAA predicted tide data |
| `MyCoastAI-description` | AI-generated photo description (sparse) |
| `report_created` | ISO 8601 UTC timestamp of report submission |

---

### Annotator 1 Columns (Cols 23–30)

Each annotation field is answered Y (yes) or N (no) by the first assigned annotator. Approximately 35–37 rows are blank (not yet annotated).

#### `Training photo? (Y/N)`
- **Description:** Flags whether the photo was used as a training/example image for the class before independent tagging began. Training photos should typically be excluded from inter-rater reliability analyses.
- **Values:** `Y`, `N`, `N?`, `?`
- **Notes:** Uncertain responses (`N?`, `?`) indicate annotator was unsure.

#### `Ocean? (Y/N)`
- **Description:** Is the ocean (open saltwater, bay, or estuary directly connected to the ocean) visible or depicted in the photo?
- **Values:** `Y`, `N`
- **Non-null:** ~373 records

#### `River? (Y/N)`
- **Description:** Is a river, stream, or freshwater channel visible or depicted in the photo?
- **Values:** `Y`, `N`, `n` (treat as `N`)
- **Non-null:** ~373 records

#### `Street? (Y/N)`
- **Description:** Is a road, street, or paved surface visible or prominently featured in the photo?
- **Values:** `Y`, `N`
- **Non-null:** ~373 records

#### `Flooding? (Y/N)`
- **Description:** Is there visible flooding — standing water in areas that are not normally submerged — in the photo?
- **Values:** `Y`, `N`
- **Non-null:** ~373 records

#### `Elevated/Flood Alert? (Y/N)`
- **Description:** Does the photo show signs of elevated water (e.g., water at or near the top of seawalls, docks, or banks) or conditions that indicate a flood alert, even without fully inundated land?
- **Values:** `Y`, `N`
- **Non-null:** ~373 records

#### `Damage? (Y/N)`
- **Description:** Is there visible physical damage to infrastructure, property, or the natural environment in the photo?
- **Values:** `Y`, `N`
- **Non-null:** ~349 records; more missing than other tags, suggesting some annotators skipped this field more often.

#### `Comments`
- **Description:** Free-text notes from Annotator 1, used to flag ambiguous photos or explain tagging decisions.
- **Examples:** `"Damage not visible"`, `"Fallen branch on left"`, `"Flooding in walkway"`
- **Non-null:** ~58 records (~14%)

---

### Annotator 2 Columns (Cols 31–38)

Identical set of annotation fields completed independently by a second annotator for inter-rater reliability. Column names are appended `.1` by pandas when read programmatically (e.g., `Training photo? (Y/N).1`).

All fields mirror Annotator 1 exactly. Key differences to note:
- `Elevated/Flood Alert? (Y/N)` contains lowercase `y` entries (16 records) — treat as `Y`.
- `Flooding? (Y/N)` contains one lowercase `y` — treat as `Y`.
- `Training photo? (Y/N)` contains `Y?` entries (4 records) indicating uncertainty.
- Approximately 40–43 rows are blank.

---m

## Sheet 3: `MyCoast export 2026-02-07`

**Purpose:** The full raw data export from the MyCoast platform https://mycoast.org/, exported February 7, 2026. This is the source data underlying the Tagging sheet.

**Records:** 410 rows  
**Columns:** 83  
**Report types:** King Tide (259), Storm Reporter (148), Coastal Resilience (3)  
**Photo date range:** 2006-03-30 to 2026-01-25

---

### Core Report Fields

#### `ID #`
- **Type:** Integer
- **Description:** Unique identifier assigned by MyCoast to each report.
- **Missing:** None

#### `reportType`
- **Type:** String (categorical)
- **Description:** The type of observation program through which the report was submitted.
- **Values:** `King Tide` (259), `Storm Reporter` (148), `Coastal Resilience` (3)

#### `photo_date`
- **Type:** Date (`YYYY-MM-DD`)
- **Description:** Date the photo was taken, based on device EXIF data or user input.
- **Range:** 2006-03-30 to 2026-01-25
- **Missing:** None

#### `photo_time`
- **Type:** Time (`H:MM am/pm`)
- **Description:** Time the photo was taken.
- **Missing:** None

#### `report_created`
- **Type:** String (ISO 8601 UTC datetime)
- **Description:** Timestamp when the report was submitted to MyCoast.
- **Missing:** None
- **Notes:** May differ from `photo_date`/`photo_time` if photo was taken earlier and submitted later.

#### `from_device`
- **Type:** String
- **Description:** Operating system and version of the submission device.
- **Examples:** `iOS 14.8`, `Android 9`
- **Missing:** Some records

#### `AuthorName` / `AuthorEmail`
- **Type:** All null
- **Description:** Submitter identity fields — fully redacted in this export for privacy.

#### `URL`
- **Type:** String (URL)
- **Description:** Public permalink to the report on mycoast.org.
- **Missing:** None

#### `images`
- **Type:** String (pipe-delimited URLs)
- **Description:** One or more image URLs, separated by `|`.
- **Missing:** A small number of records

#### `report_icon`
- **Type:** String
- **Description:** Icon file used to represent this report type on the MyCoast map.
- **Values:** `tide.svg`, `nuisance.svg`, `storm.svg`, `resilience.svg` (varies by report type)
- **Missing:** None

#### `embed`
- **Type:** All null in this export.

---

### Location Fields

#### `location_longitude` / `location_latitude`
- **Type:** Float (decimal degrees, WGS 84)
- **Description:** GPS coordinates of the report.
- **Missing:** None

#### `geo_administrative_area_level_1`
- **Type:** String — State abbreviation from reverse geocoding.

#### `geo_administrative_area_level_2`
- **Type:** String — County from reverse geocoding.

#### `geo_locality`
- **Type:** String — City or town from reverse geocoding.

#### `geo_neighborhood`
- **Type:** String — Neighborhood from reverse geocoding. Missing for some locations.

#### `geo_route`
- **Type:** String — Street name from reverse geocoding. Missing for some locations.

#### `place_name`
- **Type:** String (free text)
- **Description:** Named location entered by the submitter, distinct from the automatic geocoding fields.
- **Examples:** `Hurricane Barrier`, `Fox Point Hurricane Barrier`, `Pawtuxet Neck, Cranston`
- **Non-null:** 61 records (15%)

---

### Weather Fields
*(Auto-fetched at time of submission based on location and timestamp)*

#### `weather_temperature`
- **Unit:** °F
- **Description:** Ambient air temperature at time of submission.

#### `weather_windSpeed`
- **Unit:** mph
- **Description:** Wind speed at time of submission.

#### `weather_windBearing`
- **Unit:** Degrees (meteorological: direction wind is coming *from*; 0/360=N, 90=E, 180=S, 270=W)
- **Description:** Wind direction at time of submission.

#### `weather_calc_24hr_precip`
- **Unit:** Inches
- **Description:** Calculated total precipitation in the 24 hours preceding submission.

---

### Tide Fields

#### `TideDataObserved`
- **Type:** String (URL)
- **Description:** Link to NOAA observed water level data for the nearest gauge, centered on the report date (±1 day). Datum: MLLW; units: standard (feet).

#### `TideDataPredicted`
- **Type:** String (URL)
- **Description:** Link to NOAA predicted tide chart for the same gauge and date window.

---

### Narrative / AI Fields

#### `post_comment`
- **Type:** String (free text)
- **Description:** Written description provided by the submitter at time of report.
- **Non-null:** 130 records (32%)

#### `MyCoastAI-description`
- **Type:** String (free text)
- **Description:** Automated AI-generated description of the photo(s).
- **Non-null:** 129 records (31%)

---

### Storm Damage & Response Fields
*(Structured fields from the Storm Reporter report type; most are sparsely populated in this dataset)*

| Column | Description | Non-null |
|---|---|---|
| `storm_damage` | Overall: was storm damage observed? (Y/N) | 149 |
| `road_damage` | Damage to roads? (Y/N) | 137 |
| `storm_streetroad` | Name/location of impacted road (free text) | 4 |
| `road_damage_detail` | Severity: `Impacted, but passable` or `Impassable (flood water)` | 5 |
| `road_impact_detail` | Short code for road impact type | 3 |
| `road_other` | Other road damage description | 0 |
| `road_comments` | Free-text road comments | 1 |
| `marinas_damage` | Damage at marinas? (Y/N) | 76 |
| `marinas_damage_detail` | Type: e.g. `Damaged piers/docks` | 2 |
| `marinas_comments` | Free-text marina comments | 0 |
| `float_number` | Number of damaged floats | 73 |
| `boat_number` | Number of damaged boats | 73 |
| `buildings_damage` | Damage to buildings? (Y/N) | 76 |
| `buildings_street` | Address of damaged building | 0 |
| `buildings_damage_detail` | Type of building damage | 0 |
| `buildings_comments` | Free-text building comments | 0 |
| `hazmat_damage damage-cat` | Hazardous materials release? (Y/N) | 132 |
| `hazmat_damage` | Secondary hazmat flag (Y/N) | 5 |
| `hazmat_damage_detail` | Type: e.g. `Other large debris` | 1 |
| `hazmat_damage_detail_other` | Free-text hazmat detail | 0 |
| `hazmat_comments` | Free-text hazmat comments | 0 |
| `beach_damage` | Beach damage? (Y/N) | 76 |
| `beach_comments` | Free-text beach comments | 2 |
| `structure_damage` | Damage to structures (docks, seawalls)? (Y/N) | 76 |
| `structures_damage` | Duplicate/secondary structure damage flag | 0 |
| `structure_damage_detail` | Type: e.g. `Damaged stairs/walkovers` | 1 |
| `structures_comments` | Free-text structure comments | 1 |
| `natural_damage` | Natural/environmental damage? (Y/N) | 137 |
| `natural_damage_detail` | Type of natural damage | 0 |
| `natural_comments` | Free-text natural damage comments | 0 |
| `response_damage` | Emergency response observed: e.g. `Road clearing`, `Utility repair` | 2 |
| `response_other` | Other response description | 0 |
| `access_damage` | Access impacted? (Y/N) | 1 |
| `access_impacts` | Type of access impact: e.g. `other` | 1 |

---

### Flooding Detail Fields

| Column | Description | Non-null |
|---|---|---|
| `flooding_cause` | Cause of flooding: `Rainfall`, `Clogged Storm Drain` | 26 |
| `flooding_cause_other` | Free-text flooding cause | 0 |
| `flooding_what` | What was flooded: `Roads/street`, `Sidewalk` | 12 |
| `flooding_what_other` | Free-text flooding location | 0 |
| `est_water_depth` | Estimated water depth: e.g. `About the height of a curb` | 3 |

---

### Coastal Resilience / Site Assessment Fields
*(From the Coastal Resilience report type; very sparse — only ~2–3 records)*

| Column | Description | Non-null |
|---|---|---|
| `site_type` | Physical site type: e.g. `beach (sandy)` | 2 |
| `infrastructure` | Type of coastal infrastructure: `revetment`, `bulkhead/seawall`, `other` | 3 |
| `stability` | Shoreline stability: `eroding`, `unknown` | 2 |
| `vegetative_cover_amount` | Amount of vegetation: `moderate`, `sparse` | 2 |
| `dominant_vegetation` | Dominant plant type: e.g. `grasses` | 2 |
| `dominant_vegetation_type` | More specific vegetation type | 0 |
| `unanchored_components` | Loose materials present: e.g. `coir rolls`, `rocks` | 2 |
| `fea_limit_visibilty` | Feature limiting visibility (numeric flag) | 1 |
| `other_displaced_materials` | Displaced materials description | 0 |
| `monitoring_data` | Monitoring data notes | 0 |
| `photo_description` | Submitter's site description | 2 |
| `project_elevation` | Elevation zone: e.g. `between MHW and mean low water (MLW)` | 1 |
| `other_obstruction` | Obstruction type: e.g. `Boat ramp` | 1 |
| `other_human_impacts` | Human impacts noted: e.g. `Trash washing into marsh` | 1 |
| `marine_traffic_impacts` | Marine traffic impacts: e.g. `wrack` | 1 |

---

### Administrative Fields

#### `import_processed`
- **Type:** Float
- **Description:** Flag indicating the record was processed through an import pipeline (value `2.0`).
- **Non-null:** 5 records — likely the Coastal Resilience reports imported from another system.

---

## Notes on the Workbook

- **Two annotators per report:** The `MyCoast Tagging` sheet is designed for inter-rater reliability analysis. Disagreements between Annotator 1 and Annotator 2 should be resolved before using the labels for modeling.
- **Case inconsistencies in annotations:** Some annotators used lowercase (`y`, `n`) or uncertain entries (`Y?`, `N?`, `?`). These should be cleaned before analysis — lowercase variants can be uppercased; uncertain responses should be handled with a defined protocol (e.g., treated as missing or coded separately).
- **Sparse Storm Reporter fields:** Most structured damage fields are null for the majority of records. These fields are primarily meaningful for the 148 Storm Reporter submissions.
- **Privacy:** `AuthorName`, `AuthorEmail`, and `embed` are entirely null — redacted in this export.
- **Tagging sheet vs. export sheet:** The tagging sheet omits a few columns present in the export (author fields, `post_comment`, `report_icon`, `embed`) and uses slightly simplified column formatting for readability in a class context.
