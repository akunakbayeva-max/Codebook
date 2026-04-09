# Flood Data Codebook
### A Data Infrastructure Project for AI-Assisted Coastal Flood Prediction in Rhode Island

This repository contains a structured codebook of data sources relevant to coastal flood prediction in Providence, Rhode Island. It was developed as part of a semester-long community partnership with **VECINA**, an organization working with and for Latin-American communities in Rhode Island. The codebook is intended to serve as a foundation for future student teams and researchers building flood prediction models.

---

## Repository Contents

| File | Description |
| :--- | :--- |
| `MyCoast_KingTide_Codebook.md` | Codebook for MyCoast citizen-reported King Tide observations (Providence, RI) |
| `MyCoast_Storm_Report_Data.md` | Codebook for MyCoast citizen-reported Storm Report observations (Rhode Island) |
| `NOAA_codebook.md` | Codebook for NOAA Storm Events Database (Providence County, RI) |
| `VECINA_MyCoast_Codebook.md` | Codebook for VECINA-specific MyCoast data |


---

## Project Background

Coastal flooding is a growing concern for Rhode Island communities, particularly in Providence. Existing data on flooding events is scattered across multiple platforms : citizen reports, traffic cameras, weather services, and historical databases,  with no unified reference for researchers or community organizations trying to build predictive tools.

This project addresses that gap by cataloging and documenting the most relevant data sources for flood prediction, with enough detail that future teams can quickly understand, access, and work with each dataset. The codebook is designed to be a living document that can be extended as new data sources are identified.

---

## Data Sources Covered

The codebook covers four primary categories of flood-relevant data:

**Observational**
- MyCoast RI (King Tide and Storm Report modules) & VECINA MyCoast - citizen-submitted georeferenced flood photos with auto-appended tidal and weather metadata

**Meteorological & Historical**
- NOAA Storm Events Database - historical storm and flooding records for Providence County

---

## Contributors

**Nokutenda Zuze** — Math & Digital and Computational Studies (DCS), Bates College

**Alina Kunakbayeva** — Psychology & Digital and Computational Studies (DCS), Bates College

---

## Advisors & Community Partners

This project was developed in partnership with **VECINA**, a Rhode Island-based organization focused on coastal flood resilience and AI-assisted flood warning systems.

**Community Partner Mentors:**
- **Paige** — Bates & VECINA
- **Casey** — VECINA
- **Joe** — VECINA

**Course Instructor:** Carrie Diaz Eaton - Bates College (DCS Community Partnership Course)

---

## Future Aspirations

Given the time constraints of a single semester, several directions we explored had to be set aside:

- **Scraping RI DOT camera footage** - We identified the DOT camera network as a valuable real-time data stream and explored scraping screenshots programmatically. This turned out to be technically complex and was not feasible within the project timeline, but is a strong candidate for a future team to pursue.

- **Building an AI flood prediction model** - Our original project pitch involved using machine learning to identify flooding patterns across the MyCoast dataset. As we worked with the data, it became clear that a well-documented codebook was a necessary prerequisite — the model-building phase remains future work.

- **Integrating emergency alert data** - We investigated whether public emergency flood alerts could be scraped or accessed as a data stream, but could not find a clean, structured source within scope.

- **Broader geographic coverage** - Several of our codebooks are scoped to Providence only due to data availability. Expanding coverage to other coastal RI municipalities (e.g., Narragansett, Westerly, Newport) would make the codebook significantly more useful for statewide flood prediction.

- **Cross-source validation** - We noted that many RI flood data sources draw from the same underlying inputs, making it difficult to treat them as independent signals. A rigorous analysis of source independence and overlap would strengthen any future predictive model built on this codebook.

---

## How to Use This Codebook

Each `.md` file in this repository documents a single data source and follows a consistent structure:

1. **Dataset Overview** - title, source, geographic scope, time range, and data type
2. **Source & Access Information** - data producer, access method, license, and citation format
3. **Variable Descriptions** - table of all variables with type, value range, missing codes, and notes
4. **Missing Data Codes** - standardized codes used across the dataset
5. **Data Notes & Limitations** - known quality issues, caveats, and appropriate use cases
6. **Relationship to Other RI Flood Tools** - how the source connects to STORMTOOLS, RI-CHAMP, NOAA gauges, and other platforms
7. **Documentation Reference** - standards followed (Penn Libraries Data Management; ISO 8601)

---

## Citation

Penn Libraries Data Management Documentation Standards were followed in preparing these codebooks.

MyCoast: Rhode Island [dataset]. University of Rhode Island Coastal Resources Center / Rhode Island Sea Grant. https://mycoast.org/ri

NOAA Storm Events Database. National Centers for Environmental Information. https://www.ncei.noaa.gov/stormevents/
