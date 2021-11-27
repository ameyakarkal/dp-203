# 1. Design a data storage structure
Reference : https://www.youtube.com/playlist?list=PL-oeM7CaGtVjRgNJ5oy9xbrpcOYr3RhZG
Reference : https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-best-practices
## 1.1 design an Azure Data Lake solution

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

## 1.2 recommend file types for storage
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

## 1.3 recommend file types for analytical queries
    - raw : JSON / csv
    - non raw : parquet / databricks delta lake format
## 1.4 design for efficient querying
Reference : https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-query-acceleration
 - query acceleration, application can provide filter predicates and projection predicates
 - processors filter and stream out only the data that match the predicate, reducing transfer of unwanted data
 
## 1.5 design for data pruning
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
## 1.6 design a folder structure that represents the levels of data transformation
    - raw
    - cleaned
    - lab
    - curated
    - sensitive

## 1.7 design a distribution strategy
- Reference : [Design Principles for Partitioning with Azure](https://app.pluralsight.com/library/courses/design-principles-partitioning-azure/table-of-contents)
- Partitioning
    - Key Concepts
        - performance
        - scalability : needs to support 
        - availability
    - Horizontal Paritioning | Sharding
        - each partition has same schema
        - define a partitioning key. (e.g : tenantId)
        - rows are partitioned
    - Vertical Partitioning
        - different schema
        - bring columns with similar concerns like GDPR, sensitivity level, authentication together, slowly changing properties
    - Functional Partitioning 
        - microservices | bounded context define a partition
        - partitioning for performance (archive vs current)
- Choosing good partitioning key (horizontal partitioning)
    - key should have ~high cardinality
    - key should be static (avoid shuffling of data after creation)
    - key should distribute frequency evenly. NOT create UNEVEN Shards
    - key should distribute load evenly. NOT create HOT partitions
- Use Cases
    - Auditing and masking of PII data : vertical
    - Improve write complexity of queries : bounded context : functional
    - Disaster recovery : horizontal : horizontal
## 1.8 design a data archiving solution
