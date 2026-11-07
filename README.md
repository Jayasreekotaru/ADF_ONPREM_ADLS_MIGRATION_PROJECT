# ADF_ONPREM_ADLS_MIGRATION_PROJECT
This project demonstrates an end-to-end data migration solution using Azure Data Factory (ADF) to ingest data from an On-Premises SQL Server into ADLS Gen2.The solution implements an incremental loading framework using a watermark table to efficiently migrate only new or changed records, reducing data movement and improving pipeline performance.

**Architecture**

**Parent Pipeline (Orchestration Layer)**

The parent pipeline controls the overall execution process.

  Reads source table metadata from the Watermark Table.  
  Iterates through each table using a ForEach activity.
  
  Executes the Incremental Load Child Pipeline for every table.
  
**Child Pipeline (Incremental Load Logic)**
  
The child pipeline performs incremental data processing.

  Retrieves the latest watermark value from the source table.
  
  Compares the current watermark value with the previously loaded watermark value.
  
  Checks whether new records are available.
  
  Performs Full Load or Incremental Load based on the evaluation.
  
  Loads data from SQL Server to ADLS Gen2 in Parquet format.
  
  Invokes the Stored Procedure Pipeline after successful ingestion.
  
**Child Pipeline (Stored Procedure)**

Responsible for maintaining watermark tracking.

  Executes the dbo.UpdateWatermark stored procedure.
  
  Updates the LastLoadValue in the watermark table.
  
  Prepares the framework for future incremental executions.

**End-to-End Flow**

**ADF Watermark Table → Lookup Metadata → ForEach Activity → Execute Child Pipeline → Lookup MAX(WatermarkColumn) → Validate New Data Availability → Full Load / Incremental Load Decision → Copy SQL Server to ADLS Gen2 (Parquet) → Execute Stored Procedure Pipeline → dbo.UpdateWatermark → Update LastLoadValue → Pipeline Complete**

**Key Features**

  On-Prem SQL Server to ADLS Gen2 Migration
 
  Metadata-Driven Processing
  
  Parent-Child Pipeline Architecture
  Watermark-Based Incremental Loading
  
  Dynamic Multi-Table Ingestion
  
  Automated Watermark Updates
  
  Parquet File Generation
  
  Reusable and Scalable Framework
  

==========================================================================================
Jayasree Kotaru
