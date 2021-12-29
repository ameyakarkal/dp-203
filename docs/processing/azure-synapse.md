# Azure Synapse
Reference : https://www.youtube.com/channel/UCbEGP_wQd7VNC002upGt24g
Reference : [Pluralsight : Implement Datalakehouse with Azure Synapse](https://app.pluralsight.com/library/courses/building-first-data-lakehouse-azure-synapse-analytics/table-of-contents)
Reference : [Pluralsight : Implement Security on Azure Synapse](https://app.pluralsight.com/library/courses/implement-security-azure-synapse/table-of-contents)
## Concept
- 2015 Azure Sql Datawarehouse
- 2019 Azure Synapse Analytics
- 2020 Azure Synapse Analytics
## Architecture
- Reference
    - main reference : [Pluralsight : Implement Datalakehouse with Azure Synapse](https://app.pluralsight.com/library/courses/building-first-data-lakehouse-azure-synapse-analytics/table-of-contents)
    - additional reading : [Pluralsight : Data Literacy: Essentials of Azure Synapse Analytics](https://app.pluralsight.com/course-player?clipId=115bb506-79f6-4127-8f3c-5bf8b201ce50)
- Storage
    - Azure datalake Gen2
    - a default storage account is associated to azure synapse workspace. this could be a new storage account or existing one
- Compute
    - Azure Dedicated SQL pool
    - Serverless SQL
        - A default serverless pool is associated with workspace.
    - Apache Spark pool
- Ingestion
    - Synapse pipleine
    - mapping dataflows
- Ingetration
    - Azure Metrics
    - Azure Monitor
    - Azure log analytics
- Connected Service
    - CosmosDB
    - Power BI
- Encryption
    - At Rest
    - In Transit
## Storage
- Azure Datalake Gen2 storage account
- can be connected to multiple storage accounts
- support for DELTA LAKE and Common Data Model
## Compute
- SQL Dedicated Pool
    - Dedicated SQL pools : based on SQL MPP
    - pay for the compute even if it is not used
    - define model in T-SQL
- Apache Spark Pool
    - open source
- Dataflows
    - executed on spark cluster
    - no code approach for ETL
- Serverless SQL
    - allows to connect to external data sources : cosmosdb
    - pay for only the data processed
## Ingestion
- Synapse pipelines
    - azure data factory pipelines
    - orchestrate activities
- Mapping dataflow
## Connected Services
- cosmosdb : query without loading data
- Power BI workspace
- Azure ML : consume ml models | build and consume ML
---

# Azure Sql Dedicated Pool
- available as standalone service as Azure Datawarehouse
- distributions :
    - basic unit of data
    - data is distributed across 60 nodes
    - query is executed against each distribution
    - stored in azure storage
- control node : 
    - stores metadata
    - frontend service for client and application
    - coordinates with compute nodes
- compute nodes:
    - compute power to execute the queries
    - upto 60 compute node
    - work is balanced between compute nodes. reduces the amount of work done by each compute node
- data movement service: coordinates movement of data between compute node
- polybase based querying on external data sources
    - COMPONENTS : CREDENTIALS | DATASOURCE | FILE FORMAT | SCHEMA
    - database scoped credential
    - data source that defines the location of the external datasource
    - file format entity that defined file format
    - external table that define the schema
- copy allows to copy data from the external source to pool table
- distribution method
    - round robin : default.
    - hash : specify a column
    - replicate : table is copied to each of the compute node. use it for small dimension tables
# Serverless SQL pool
- distributed sql engine
- control node | compute node | read data from external data sources
- no provisioning infrastructure
- use 
    - external tables : datasource, datasource scoped credential, file format, schema
    - openrowset

## [Running Notebook in Pipeline](#notebook-in-pipeline)
- Reference : 
    - [youtube](https://www.youtube.com/watch?v=89m1VOXXnHM)
    - [youtube : parameters](https://www.youtube.com/watch?v=t5myJYV__Jo)
        - parameter cell.
        - data factory / synapse pipeline overwrites the parameter values

# Security
## Encryption
- at rest : uses TDE (Transparent Data Encryption) using Encryption key
    - raw data and logs are encrypted
    - PCI compliant
    - Keys
        - managed key
        - customer managed key
        - TDE proctector : managed key can be used to encrypt the Transparent Data Encryption key
- in transit : TLS : transport layer security
- using azure key vault with azure synapse
## Data Masking
- types : how a masked data column is showed
    - default : XXX
    - random : XX233XX
    - email : mask email address
    - custom : user defined
## Row and Column level security
- row level security using predicte
    - create separate schema 
    - create predicate table valued function
    - create security policy : assigns tvf to a table
    - grant select access on tvf for the user
- column level security : grant access to the user
    - user gets error when projecting columns that don't fall in the grant scope

## [Monitoring using DMV](#monitoring-dvm)
- Reference 
    - [docs](https://docs.microsoft.com/en-us/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-manage-monitor)

- `dm_pdw_exec_sessions` : active sessions | session_id() gives the current session
- `dm_pdw_exec_requests` : queries that are run. `total_elaspsed_time` | run query with `OPTION (LABEL='My Label')`
- `dm_pdw_request_steps` : query plan
- `dm_pdw_dms_workers`   : find how data is moving | find which distribution is causing waits
- `dm_pdw_waits`         : joins with `dm_pdw_requests` | find which request is waiting for a specific resource
- monitor tempdb         : 
    - failure in CTAS / INSERT SELECT can cause tempdb to build. this is used to save intermediate results
    - involves querying `nodes_exec_sessions` `nodes_exec_requests` and `nodes_sessions_space_usage` 
- monitor memory         :
    - needs to be calculated at the node level
    - node_os_performance_counters
- transaction log
    - log size : `node_os_performance_counters`
    - rollback :  `node_tran_database_transactions`
- polybase memory usage
    - `pdw_dms_external_work` 
---
## Deep Dive
[yuotube play list : https://www.youtube.com/c/ArshadAliAasTrailblazers/videos](https://www.youtube.com/c/ArshadAliAasTrailblazers/videos)
- Partitioning
- Distribution
- Index
    - heap : best for fast insert
    - column store : 
        data->row group (1 million rows) -> column -> column segment -> (compression) -> column store
    - clustered index : specified with a column to be used for clustered index
    - non clustered index : created on top of heap / clustered index table


## External table
- create credentials
    - identity
        - SHARED ACCESS SIGNATURE
        - MANAGED IDENTITY
```sql


CREATE DATABASE SCOPED CREDENTIAL blobUser
WITH
    IDENTITY='identity',
    SECRET =  'SHA'
```

- create datasource
    - 
```sql  
CREATE EXTERNAL DATASOURCE core_data
WITH 
    (
        LOCATION = 'prefix://path'
    )
```