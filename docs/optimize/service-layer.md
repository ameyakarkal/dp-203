# Service Layer
## Reference 
- [Design Principles for Serving Layer in Microsoft Azure](https://app.pluralsight.com/library/courses/design-principles-serving-layer-microsoft-azure/table-of-contents)
## Concept

<pre>
    datasources 
        -> Data Store 
            -> Processing 
                -> Analytics Data Store 
                    -> Consumer
</pre>

- Data Stores
    - Key Value
    - Document
    - Column family : data is stored as families of columns
    - Graph : data is stored as object and relations
    - Time series : append only
## Analytics Data Store
### Key Constraints
### Implementation
    - Azure Synapse Analytics
        - Sql 
        - Spark
        - Pipeline
        - Integration with other azure service
    - Databricks
        - Sql
        - ML
        - Data Science
    - Azure Data Explorer
        - Time series data
    - Azure Sql DB
    - SQL Server on VM
    - HDInsight (managed service)
        - Apache Hadoop
    - Azure Analytics Service
    - Azure Cosmos DB
## Consumption Platform
### Criteria for Selection

- Support for different analytics data stores / data sources
- embed reports
- offline design of reports
- size of dataset

### Implementation
- Power BI
- Jupyter Notebooks
- Zepplin Notebooks
    - HDInsight come preconfigured
- Microsoft Azure Notebooks

## Implementation Design

### Star Schema
- Fact Table
- Dimension Table
    - Type 1 SCD
        - dimension changes.
        - key of the dimension does not change over time
    - Type 2 SCD
        - dimension changes
        - key changes
        - surrogate key is used for reference in fact table
        - start/end date / IsCurrent flag used to identify current version
        - if the source system does not store changes, intermediate data store is used for capturing the change in the dimension
    - Type 3 SCD
        - dimension changes
        - key remains same
        - old and new columns are maintained on the same dimension record. e.g OldEmail|CurrentEmail
    - Type 6 SCD
        - combination 1/2/3
        - dimension changes
        - key changes
        - surrogate key is used
        - old and new columns are on the dimension
        - start/end date/ Is Current flag used to identify current version

### Demo : Analytics Synaptics 
- create resource group
- create analytics workspace
- create security account
- create sql pool
    - create source table (loads data from files)
    - create dimension table (loads data using mapping data flow from source table)
    - create mapping data flow

