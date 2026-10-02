# Adverse Event (AE) Log Tracker and Data Quality Monitoring Tool

An Excel-based tool that simulates how clinical data teams log adverse events (AEs) and run a first-pass data quality check before database lock. It automatically flags missing fields, misclassified serious AEs, and fatal outcomes that need escalation. The data structure is modelled on the FDA Adverse Event Reporting System (FAERS).



![AE Log with auto-flags](docs/screenshots/02-ae-log-autoflags.jpg)



**Note:** All data in this project is simulated for portfolio use. No real patient data is used.

## Project at a Glance

- **Role:** Clinical Data Analyst (independent portfolio project)
- **Tool:** Microsoft Excel
- **Dataset:** 52 simulated AE records from a fictional Phase III oncology trial across 4 sites
- **Core feature:** Formula-driven AUTO-FLAG column that checks every record for completeness and classification errors
- **Output:** A four-sheet workbook with a data entry log, dropdown reference lists, and a live summary dashboard
- **Standards applied:** ICH E6(R2) GCP, ICH E2A seriousness criteria, CTCAE severity grading, FAERS data structure

## The Problem This Solves

Clinical data teams manually review AE logs for completeness and accuracy before database lock. Missed flags can lead to protocol deviations and potential regulatory issues, and reviewing hundreds of rows by eye is slow and error-prone.

This tool automates that first-pass check. A reviewer can open the log, see immediately which records are clean, which need a query to the site, and which need urgent escalation.

## Trial Context

- **Study type:** Fictional Phase III oncology trial
- **Sites:** 4 (S-01 to S-04)
- **Period:** Q1 2024
- **Records:** 52 AE entries
- **Data structure:** Modelled on FDA FAERS
- **Severity grading:** CTCAE, Grade 1 (Mild) to Grade 5 (Fatal)
- **Seriousness:** ICH E2A seriousness criteria

## Methodology

1. **Designed the data structure** using FAERS as the model, selecting the fields a reviewer needs to assess each event
2. **Built standardised reference lists** for severity, system organ class, seriousness criteria, outcome, and relatedness
3. **Applied data validation** so coded fields use dropdown menus instead of free text
4. **Created a raw dataset with deliberate errors**, such as missing onset dates, missing severity grades, and serious events with no criteria. The errors were highlighted in yellow so I could test the tracker against known problems
5. **Wrote the AUTO-FLAG logic** to check each record against defined data quality rules
6. **Added conditional formatting** so problem rows stand out in green, yellow, and red
7. **Built a summary dashboard** with metrics and breakdown tables that update automatically
8. **Tested the flags** against the planted errors to confirm they were caught

## The Input Dataset

Before building the tracker, I created a raw AE dataset containing deliberate data quality issues (highlighted in yellow). This simulates the messy data a Clinical Data Associate receives and gave me a way to confirm the tracker works.



![Raw AE dataset](docs/screenshots/05-raw-dataset.jpg)





![Dataset notes and field legend](docs/screenshots/06-notes-and-legend.jpg)



## Workbook Structure

The workbook has four sheets:

- **README:** In-workbook guide covering what the tool does, the problem it solves, how to use it, and the flag legend
- **AE LOG:** Main data entry sheet, one row per AE, with an AUTO-FLAG column
- **Reference Lists:** Source lists that power the dropdown menus
- **Summary Dashboard:** Auto-calculated metrics and breakdown tables



![README sheet](docs/screenshots/01-readme-sheet.jpg)



## Data Fields

- **Subject ID:** Unique patient identifier (format PT-XXX)
- **Site ID:** Trial site, S-01 to S-04
- **AE Description:** The adverse event term
- **System Organ Class:** Body system category (dropdown)
- **Onset Date:** Date the AE started
- **Resolution Date:** Date the AE resolved
- **Severity Grade:** CTCAE Grade 1 to 5 (dropdown)
- **Serious? (Y/N):** Y means the event meets ICH E2A seriousness criteria
- **Seriousness Criteria:** Required whenever Serious = Y (dropdown)
- **Relatedness to Drug:** Investigator's causality assessment (dropdown)
- **Outcome:** Patient status at time of report (dropdown). Fatal requires immediate escalation
- **Reported By:** Investigator or CRA who reported the event
- **Date Reported:** Date the AE was reported
- **AUTO-FLAG:** Formula-driven data quality status

## Reference Lists

Dropdowns are driven by a dedicated sheet so every entry is standardised and free-text errors are avoided.

- **Severity Grade:** Grade 1 - Mild, Grade 2 - Moderate, Grade 3 - Severe, Grade 4 - Life-Threatening, Grade 5 - Fatal
- **System Organ Class:** Cardiac, Gastrointestinal, General, Infections and Infestations, Nervous System, Respiratory, Skin, Vascular
- **Seriousness Criteria:** Hospitalization, Life-Threatening, Death, Disability or Incapacity, Congenital Anomaly, Other Medically Important
- **Outcome:** Recovered / Resolved, Recovering / Resolving, Not Recovered / Not Resolved, Fatal, Unknown
- **Relatedness:** Certain, Probable, Possible, Unlikely, Not Related
- **Serious?:** Y, N



![Reference lists](docs/screenshots/04-reference-lists.jpg)



## Auto-Flag Logic

The AUTO-FLAG column checks every row and returns one of six statuses:

- **Complete:** No issues detected. The record is ready for review.
- **Warning - Missing Onset Date:** Onset date is blank, so the AE cannot be placed on the study timeline.
- **Warning - Missing Severity Grade:** Severity grade is blank, so severity and seriousness cannot be assessed.
- **Warning - Serious AE, No Criteria Entered:** Serious? = Y but no seriousness criteria were recorded. ICH E2A requires the criteria to be documented.
- **Warning - Grade 4 Should be Serious:** The event is Grade 4 (Life-Threatening) but marked as non-serious. This is a likely misclassification and needs a query to the site.
- **Critical - Fatal, Escalate Immediately:** Outcome = Fatal. This requires immediate escalation.

Conditional formatting colours these green, yellow, and red so that problem rows stand out at a glance.

AUTO-FLAG formula used:

(Paste your formula from cell N3 here)

## Summary Dashboard

The dashboard updates automatically as entries are added or corrected.



![Summary dashboard](docs/screenshots/03-summary-dashboard.jpg)



**Headline metrics:**

- **Total AEs logged:** 52
- **Serious AEs:** 20 (about 38% of all events)
- **Fatal AEs:** 3
- **Flagged entries:** 17
- **Data completeness rate:** 67.3%

**Breakdown tables:** AEs by System Organ Class, AEs by Severity Grade, and AEs by Outcome, each with counts and percentage of total.

## Key Findings

- 17 of 52 records (about one third) were flagged, which gives a data completeness rate of 67.3%. This shows how much cleaning work a dataset like this would need before database lock.
- 20 of 52 events were classified as serious, and 3 had a fatal outcome, each requiring immediate escalation.
- Severity was spread across all grades: Grade 1 (12), Grade 2 (13), Grade 3 (11), Grade 4 (9), Grade 5 (2).
- General Disorders was the largest system organ class, with 13 AEs.
- 20 events (38%) recovered or resolved, while 13 (25%) were not recovered or not resolved at the time of report.

## Real-World Relevance

This project simulates tasks performed in clinical data management and pharmacovigilance:

- Reviewing AE data for completeness and consistency before database lock
- Identifying records that need a data query to the investigator site
- Checking that seriousness classification follows ICH E2A criteria
- Escalating fatal outcomes immediately
- Using standardised dictionaries and dropdowns to keep data consistent

## Skills Demonstrated

- Clinical data review and query identification
- AE severity and seriousness assessment
- Risk-based data monitoring
- Data quality monitoring and validation logic
- Excel formulas, data validation, and conditional formatting
- Spreadsheet automation and dashboard design
- Understanding of GCP, ICH E2A, CTCAE, and FAERS
- Technical documentation

## How to Use

1. Download AE_Log_Tracker.xlsx from the tracker folder
2. Open it in Microsoft Excel (no macros required)
3. Go to the AE LOG sheet
4. Enter or paste AE data, using the dropdown fields for coded values
5. Check the AUTO-FLAG column and fix any warning or critical entries
6. Open the Summary Dashboard for real-time metrics

## Limitations

- The data is simulated and the field set is simplified. This is not a full EDC system.
- Events are classified to System Organ Class only, with no term-level MedDRA coding.
- Excel provides no audit trail, unlike a validated EDC system.
- The flags check completeness and consistency, not clinical correctness.

## Future Improvements

- Add a cross-check that an Outcome of Fatal corresponds to Grade 5 severity
- Add date logic to catch resolution dates earlier than onset dates
- Add MedDRA-style term coding
- Add SAE reporting timeline tracking (for example, 24-hour reporting)
- Build a Power BI version of the dashboard for trend monitoring

## Standards and References

- ICH E6(R2) Good Clinical Practice
- ICH E2A: Clinical Safety Data Management, definitions and standards
- CTCAE severity grading
- FDA Adverse Event Reporting System (FAERS) Public Dashboard: https://www.fda.gov/drugs/questions-and-answers-fdas-adverse-event-reporting-system-faers/faers-public-dashboard

