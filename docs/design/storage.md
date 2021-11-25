# Design a data storage structure
Reference : https://www.youtube.com/playlist?list=PL-oeM7CaGtVjRgNJ5oy9xbrpcOYr3RhZG
Reference : https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-best-practices
## - [x] design an Azure Data Lake solution

- [x] performance : tier : hot | cold | archive
- [x] replication 
    - LRS : three copies are created in ONE region under ONE zone (data center)
    - ZRS : three copies are created in ONE region across THREE zones (data centers)
    - GRS : 
        - three copies are created in ONE region under ONE zone (data center)
        - three copies are created in another region under ONE zone (data center)
        - read/write on primary | fail over which takes an hour needed to read from secondary
    - GZRS : 
        - three copies are created in ONE region across THREE zones (data centers)
        - three copies are created in another region under ONE zone (data centers)
        - read/write on primary | fail over which takes an hour needed to read from secondary
    - RA-GRS : same as GRS with secondary read
    - RA-GZRS : same as GZRS with secondary read
- [x] organization and file types
    - zones
        - raw       : json, csv
        - silver    : json, csv
        - gold      : parquet, delta-lake

## - [x] recommend file types for storage
    - relational
        - azure sql db
        - postgres
        - mysql
        - mariaDB
    - columnar
        - azure analysis
        - power bi
        - azure sql columnar index
        - cosmosdb casandra api
    - graph
        - cosmosdb gremlin api
        - azure sql db graph tables
    - key value
        - storage table
        - redis cache 
        - cosmosDB
    - object
        - azure storage account blob
        - adls gen1 | adls gen2
    - time series
        - azure data explorer | time series insights

## - [x] recommend file types for analytical queries
    - raw : JSON / csv
    - non raw : parquet / databricks delta lake format
## [ ] design for efficient querying
Reference : https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-query-acceleration
 - query acceleration, application can provide filter predicates and projection predicates
 - processors filter and stream out only the data that match the predicate, reducing transfer of unwanted data
 
## - [x] design for data pruning
- storage account gen2 : life cycle management
- azure sql edge : define data_retention_policy on database and table
```sql
alter database [db1] set DATA_RETENTION ON;

create table Table_01
(
    Id int primary key,
    CreatedOn datetime,
)
WITH (
    DATA_RETENTION = ON (FILTER_COLUMN = CreatedOn, RETENTION_PERIOD =1 DAY)
)
```
## - [x] design a folder structure that represents the levels of data transformation
    - raw
    - cleaned
    - lab
    - curated
    - sensitive

## - [ ] design a distribution strategy


## - [ ] design a data archiving solution
