# dp-203
- Design and implement data storage (40-45%)
- Design and develop data processing (25-30%)
- Design and implement data security (10-15%)
- Monitor and optimize data storage and data processing (10-15%)

## Reference 
- https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4MbYT
- [exam overview](https://www.youtube.com/watch?v=-FUMomndiLo&t=20s)

# Design and Implement Data Storage (40-45%)

[Design a data storage structure](docs/design/overview.md)
- [x] [design an Azure Data Lake solution](docs/design/overview.md#design)
- [x] [recommend file types for storage](docs/design/overview.md#filetype)
- [x] recommend file types for analytical queries
- [x] [design for efficient querying](docs/design/overview.md#design-data-querying) 🔎
- [x] [design for data pruning](docs/design/overview.md#design-data-pruning) ❌ 
- [x] [design a folder structure that represents the levels of data transformation](docs/design/overview.md#folder)
- [x] [design a distribution strategy](docs/design/overview.md#design-data-distribution)
- [x] [design a data archiving solution](docs/design/overview.md#design-data-archive)

[Design a partition strategy](docs/design/overview/#partitioning)

optional : storage account architecture : https://sigops.org/s/conferences/sosp/2011/current/2011-Cascais/printable/11-calder.pdf

- [ ] [design a partition strategy for files](docs/design/overview/#partitioning-storage-account)
- [ ] [design a partition strategy for analytical workloads](docs/design/overview/#partitioning-synapse)
- [ ] [design a partition strategy for efficiency/performance : same as analytics workload](docs/design/overview/#partitioning-performance)
- [ ] [design a partition strategy for Azure Synapse Analytics](docs/design/overview/#partitioning-synapse)
- [ ] identify when partitioning is needed in Azure Data Lake Storage Gen2

Design the serving layer
-  design star schemas
-  design slowly changing dimensions
-  design a dimensional hierarchy
-  design a solution for temporal data
-  design for incremental loading
-  design analytical stores
-  design metastores in Azure Synapse Analytics and Azure Databricks

Implement physical data storage structures
- [x] [implement compression](docs/design/implement.md#implement-data-compress) 🗜️
- [x] implement partitioning [(refer to design distributions)](#docs/design/overview.md/design-data-distribution)
- [ ] implement sharding
- [ ] implement different table geometries with Azure Synapse Analytics pools
- [x] [implement data redundancy (refer to design redundancy)](#docs/design/overview.md/design-data-redundancy)
- [x] [implement distributions (refer to design distributions)](#docs/design/overview.md/design-data-distribution)
- [x] [implement data archiving (refer to design partitioning)](#docs/design/overview.md/design-data-distribution)

Implement logical data structures
-  build a temporal data solution
-  build a slowly changing dimension
-  build a logical folder structure
-  build external tables
-  implement file and folder structures for efficient querying and data pruning

Implement the serving layer
-  deliver data in a relational star schema
-  [deliver data in Parquet files](docs/serving-layer.md#parquet)
-  maintain metadata
-  implement a dimensional hierarchy

# Design and Develop Data Processing (25-30%)
Ingest and transform data
-  transform data by using Apache Spark
-  transform data by using Transact-SQL
-  transform data by using Data Factory
-  [transform data by using Azure Synapse Pipelines](docs/processing/azure-synapse.md)
-  [transform data by using Stream Analytics](docs/processing/azure-stream-analytics.md)
-  cleanse data
-  split data
-  shred JSON
-  encode and decode data
-  configure error handling for the transformation
-  normalize and denormalize values
-  transform data by using Scala
-  perform data exploratory analysis

Design and develop a batch processing solution
-  develop batch processing solutions by using Data Factory, Data Lake, Spark, Azure

Synapse Pipelines, PolyBase, and Azure Databricks
- [x] [create data pipelines](docs/processing/overview.md#create-data-pipeline)
- [x] [design and implement incremental data loads](docs/processing/overview.md#incremental)
- [x] [design and develop slowly changing dimensions](docs/proessing/overview.md#slowly-changing-dimension)
- [ ] handle security and compliance requirements
- [ ] scale resources
- [ ] configure the batch size
- [ ] design and create tests for data pipelines
- [ ] [integrate Jupyter/Python notebooks into a data pipeline](docs/processing/synapse.md#notebook-in-pipeline)
- [ ] [handle duplicate data](docs/processing/synapse.md#)
- [ ] handle missing data
- [ ] handle late-arriving data
- [ ] upsert data
- [ ] regress to a previous state
- [ ] design and configure exception handling
- [ ] configure batch retention
- [ ] design a batch processing solution
- [ ] debug Spark jobs by using the Spark UI

Design and develop a stream processing solution
-  develop a stream processing solution by using Stream Analytics, Azure Databricks, and

Azure Event Hubs
-  process data by using Spark structured streaming
-  monitor for performance and functional regressions
-  design and create windowed aggregates
-  handle schema drift
-  process time series data
-  process across partitions
-  process within one partition
-  configure checkpoints/watermarking during processing
-  scale resources
-  design and create tests for data pipelines
-  optimize pipelines for analytical or transactional purposes
-  handle interruptions
-  design and configure exception handling
-  upsert data
-  replay archived stream data
-  design a stream processing solution

Manage batches and pipelines
-  trigger batches
-  handle failed batch loads
-  validate batch loads
-  manage data pipelines in Data Factory/Synapse Pipelines
-  schedule data pipelines in Data Factory/Synapse Pipelines
-  implement version control for pipeline artifacts
-  manage Spark jobs in a pipeline

# Design and Implement Data Security 🔐 (10-15%)

## Design security for data policies and standards
- [x] [design data encryption for data at rest and in transit 🔐](docs/security/overview.md/#data-encryption)
- [x] [design a data auditing strategy 📒](docs/security/overview.md/#data-audit)
- [x] [design a data masking strategy 😷](docs/security/overview.md/#data-masking)
- [x] design for data privacy
- [x] [design a data retention policy 💾](docs/security/overview.md/#data-retention)
- [x] [design to purge data based on business requirements](docs/security/overview.md/#data-purge)
- [x] [design Azure role-based access control (Azure RBAC) and POSIX-like Access - [x]ntrol List (ACL) for Data Lake Storage Gen2](docs/security/overview.md/#rbac-acl)
- [x] [design row-level and column-level security 🔒](docs/security/overview.md/#row-column-security)
## Implement data security
- [x]  implement data masking
- [x]  encrypt data at rest and in motion
- [x]  implement row-level and column-level security
- [x]  implement Azure RBAC
- [x]  implement POSIX-like ACLs for Data Lake Storage Gen2
- [x]  implement a data retention policy
- [x]  implement a data auditing strategy
- [ ]  manage identities, keys, and secrets across different data platform technologies
- [ ]  implement secure endpoints (private and public)
- [ ]  implement resource tokens in Azure Databricks
- [ ]  load a DataFrame with sensitive information
- [ ]  write encrypted data to tables or Parquet files
- [ ]  manage sensitive information

# Monitor and Optimize Data Storage and Data Processing (10-15%)
## Monitor data storage and data processing
-  implement logging used by Azure Monitor
-  configure monitoring services
-  measure performance of data movement
-  monitor and update statistics about data across a system
-  monitor data pipeline performance
-  measure query performance
-  [monitor cluster performance]
-  understand custom logging options
-  schedule and monitor pipeline tests
-  [interpret Azure Monitor metrics and logs](#noop)
-  [interpret a Spark directed acyclic graph (DAG)](https://www.youtube.com/watch?v=LoFN_Q224fQ)
## Optimize and troubleshoot data storage and data processing
-  compact small files
-  rewrite user-defined functions (UDFs)
-  [handle skew in data](docs/monitor/optimize.md#skew)
-  handle data spill
-  tune shuffle partitions
-  [find shuffling in a pipeline](docs/monitor/optimize.md#find-shuffle)
-  optimize resource management
-  tune queries by using indexers
-  tune queries by using cache
-  optimize pipelines for analytical or transactional purposes
-  optimize pipeline for descriptive versus analytical workloads
-  troubleshoot a failed spark job
-  troubleshoot a failed pipeline run
