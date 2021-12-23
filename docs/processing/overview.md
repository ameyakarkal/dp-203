# Ingest and transform data
References

- Synapse Reference 01: [Pluralsight : Data Literacy: Essentials of Azure Synapse Analytics](https://app.pluralsight.com/course-player?clipId=115bb506-79f6-4127-8f3c-5bf8b201ce50)

## [1.1 create data pipeline](#create-data-pipeline)
- Synapse
  - Reference : Synapse Reference 01
  - exactly same as Azure Data Pipeline, Azure Data Mapping
- Polybase
  - ?
- Azure Databricks
  - todo
## [1.2 design and implement incremental data loads](#incremental)
- Azure Sql Db
    - Delta copy and load: control table : defines last watermark, timestamp when data was successfully copied.pipeline does a lookup, projects all data since watermark, copies to destination
    - Change Data Capture : enable change data capture on source database. copy incremental load to storage account using `SYS_CHANGE_VERSION` 
```
ALTER DATABASE <your database name>
SET CHANGE_TRACKING = ON  
(CHANGE_RETENTION = 2 DAYS, AUTO_CLEANUP = ON)  

ALTER TABLE data_source_table
ENABLE CHANGE_TRACKING  
WITH (TRACK_COLUMNS_UPDATED = ON)
```
- Azure Storage Account : copy using last modified date
## [transform data by using Azure Synapse Pipelines](#synapse-pipeline)
- Reference : 
- exactly same as Azure Data Pipeline, Azure Data Mapping

## 1.3 [design and develop slowly changing dimensions](#slowly-changing-dimension)
- type 1 : overwrite the changes. no version maintained
- type 2 : start/end date on record. single record is marked current

## 1.4 : handle security and compliance requirements