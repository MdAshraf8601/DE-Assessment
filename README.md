📄 FHIR Data Engineering Pipeline – Summary Document
🔷 Project Overview

This project implements a data engineering pipeline using Databricks and PySpark based on the Medallion Architecture (Bronze, Silver, Gold).

The pipeline processes healthcare data from a FHIR (Fast Healthcare Interoperability Resources) API and transforms it into structured, analysis-ready datasets.

🔷 Data Source

The data is sourced from the public FHIR API:

https://hapi.fhir.org/baseR4

Resources used:

Patient
Encounter
Observation
Condition

Due to network restrictions in the Databricks environment, the data was downloaded as JSON files and uploaded into Databricks Volumes for processing.

🔷 Architecture

The project follows a Medallion Architecture:

Raw JSON → Bronze → Silver → Gold → SCD Dimension
🟤 Bronze Layer
Stores raw ingested data in Delta format
Minimal transformation applied
Includes metadata such as ingestion timestamp and source
⚪ Silver Layer
Cleans and transforms the data
Flattens nested FHIR JSON structures
Selects relevant fields
Removes duplicates
🟡 Gold Layer
Provides business-level aggregated insights
Combines multiple datasets using joins
Supports analytical queries
🔷 Data Processing Steps
Data Ingestion
JSON files loaded from Databricks Volume
FHIR Bundle structure parsed
Data Transformation
Nested arrays (entry) exploded
resource fields extracted
Bronze Layer Creation
Raw structured data stored in Delta tables
Silver Layer Creation
Cleaned and flattened data
Key attributes selected
Multi-Resource Integration
Patient, Encounter, Observation, and Condition datasets processed
Gold Layer Creation
Joined datasets to generate analytics
Created summary tables (e.g., patient-level metrics)
🔷 SCD Type 2 Implementation

A Slowly Changing Dimension (SCD Type 2) approach was implemented for the Patient dimension:

Tracks historical changes in patient data
Maintains:
start_date
end_date
is_current flag

This ensures that historical records are preserved instead of overwritten.

🔷 Key Features
Handling of nested JSON (FHIR format)
Implementation of Medallion Architecture
Multi-table data integration
SCD Type 2 for historical tracking
Use of Delta Lake for storage
Scalable and modular pipeline design
🔷 Final Output

The pipeline produces analytical datasets such as:

Patient summary with:
Total encounters
Total observations
Total conditions

These outputs enable meaningful healthcare insights.

🔷 Technologies Used
Databricks
PySpark
Delta Lake
🔷 Conclusion

This project demonstrates the design and implementation of a scalable data pipeline for healthcare data using modern data engineering practices. It highlights the ability to process semi-structured data, apply transformations, and generate actionable insights.
