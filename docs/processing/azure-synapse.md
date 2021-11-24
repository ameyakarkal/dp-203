# Azure Synapse
Reference : [Implement Datalakehouse with Azure Synapse](https://app.pluralsight.com/library/courses/building-first-data-lakehouse-azure-synapse-analytics/table-of-contents)
Reference : [Implement Security on Azure Synapse](https://app.pluralsight.com/library/courses/implement-security-azure-synapse/table-of-contents)
## Concept
- 2015 Azure Sql Datawarehouse
- 2019 Azure Synapse Analytics
- 2020 Azure Synapse Analytics
## Architecture

- Storage
    - Azure datalake Gen2
- Compute
    - Azure Dedicated SQL pool
    - Serverless SQL
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