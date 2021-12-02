- [Configuring Data Security Policies in Microsoft Azure](https://app.pluralsight.com/library/courses/microsoft-azure-configuring-data-security-policies/table-of-contents)
# Data Security Policy

- Security Risks and priorities
    - what type of data are you storing
        - personal identifiable information
        - credit cards / financial data
        - user identifiable
- Compliance
- Goverance 
    - auditing
    - monitoring
    - reporting

## Data classification
    - classification : public |  internal |confidential | top secert
    - business critical : critical | non critical
    - business responsibility : department | feature
    - Implementation
        - Azure Resource Tags
            - Setup Azure Policy to enforce tags
        - Resource Type specfic tags : Advanced Data Security tag for Azure Sql
        - Azure Information Protection Labels
        - Azure Advanced SQL Data Classification
            - Security Center
                - Define level of criticality.
                - Define criteria for the tag
                - Scan database and classify tables / columns
## Data Retention
- Storage Account
    - Immutability
        - legal hold using a tag
        - immutability period defined on container using WORM (write once, read multiple)
    - Life cyle management
        - retain

# Sovereignity

## Ownership of data
- where is data stored | data is subject to laws / rules of the country where the data is collected from
- microsoft trust center


## Azure Policy and Replication
1. azure policies : restrict regions resources can be created
2. data can be replicated
   - LRS  (three replicas in same zone)
   - ZRS  (three replicas in same region across three zones)
   - GZRS (three replicas in same zone, one replica in geo sync zone)
3. SQL replication : active read geo replication | a new sql database instance needs to be provisioned in the new replication region
4. storage account replication : geo replication can be stopped at any time
5. virtual machine : geo replication enabled
   
## Azure Sentinal
- works on top of azure log analytics
- triggers 
   - detect
   - investigate
   - respond
- roles
   - Azure Sentinal Reader       : read data / incidents
   - Azure Sentinal Responder    : manage incidents
   - Azure Sentinal Contributor  : create / manage workbooks
- framework
   - connnectors  : wire up azure log analytics workspace
   - alert        : create an alert rule using Kusto Query language
   - responder    : actions to handle alerts
