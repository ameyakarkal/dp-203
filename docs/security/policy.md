# Data Security Policy


## Reference
- [Configuring Data Security Policies in Microsoft Azure](https://app.pluralsight.com/library/courses/microsoft-azure-configuring-data-security-policies/table-of-contents)


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