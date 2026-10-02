# Adverse Event (AE) Log Tracker

An Excel-based tool that simulates how clinical data teams log adverse events (AEs) and run a first-pass data quality check before database lock. It automatically flags missing fields, misclassified serious AEs, and fatal outcomes that need escalation.

**Note:** All data in this project is simulated for portfolio use. No real patient data is used.

## The Problem This Solves

Clinical Data Associates manually review AE logs for completeness and accuracy before database lock. Missed flags can lead to protocol deviations and regulatory issues. This tool automates that first-pass check.

## Trial Context

- Study type: Fictional Phase III oncology trial
- Sites: 4 (S-01 to S-04)
- Period: Q1 2024
- Records: 52 AE entries
- Data structure: Modelled on the FDA Adverse Event Reporting System (FAERS)
- Grading: CTCAE, Grade 1 (Mild) to Grade 5 (Fatal)
- Seriousness: ICH E2A criteria
