# Design and Implement Data Security (10-15%)
Reference : 
- [Implement Data Auditing Azure Data lake](https://app.pluralsight.com/library/courses/implement-data-auditing-azure-data-lake/table-of-contents)


## design

## [design data encryption for data at rest and in transit 🔐](#data-encryption)
Reference : [Azuure Encryption At Rest](https://docs.microsoft.com/en-us/azure/security/fundamentals/encryption-atrest)

Keywords : 
    - Transparent Data Encryption
    - Azure Disk Encryption
    - Keys encryption key
- encryption
    - at rest
    - in transit
- storage account
    - azure managed keys enabled by default
    - customer managed key via key vault
- azure sql database
    - server : transparent data encryption.
        - azure managed keys enabled by default
    - database : transparent data encryption
        - enable / disable encryption
- virtual machines
    - azure disk encrpytion
- key vault
    - storage for 
        - certificates
        - secrets
    - managed identities for azure services 
    - seamless integration

## [design a data auditing strategy 📒](#data-audit)
- Reference [Azure Sql - Database - Auditing](https://docs.microsoft.com/en-us/azure/azure-sql/database/auditing-overview)
- azure sql db
    - implement: auditing logs to go storage account | log analytics workspace
    - audit policy : three groups of audit logs
        - BATCH_COMPLETED_GROUP
        - FAILED_DATABASE_AUTHENTICATION_GROUP
        - SUCCESSFUL_DATABASE_AUTHENTICATION_GROUP
- azure synapse
- azure storage (similar to az-204 storage auditing)
    - implement : auditing logs -> storage account -> azure log analytics workspace -> azure monitoring

## [design a data masking strategy 😷](#data-masking)
- using TSQL / Azure Portal -> SQL DB -> Data Masking tab in Blade
- azure sql db | azure sql pool
```sql
CREATE TABLE Data.Membership(
    MemberID        int IDENTITY(1,1) NOT NULL PRIMARY KEY CLUSTERED,
    FirstName        varchar(100) MASKED WITH (FUNCTION = 'partial(1, "xxxxx", 1)') NULL,
    LastName        varchar(100) NOT NULL,
    Phone            varchar(12) MASKED WITH (FUNCTION = 'default()') NULL,
    Email            varchar(100) MASKED WITH (FUNCTION = 'email()') NOT NULL,
    DiscountCode    smallint MASKED WITH (FUNCTION = 'random(1, 100)') NULL
    );
```
- users need `GRANT UNMASK` permission on the table to view underlying data

## design for data privacy
- public
- private
- confidential

## [design a data retention policy 💾](#data-retention)
- Reference
    - [azure sql backup](https://docs.microsoft.com/en-us/azure/azure-sql/database/long-term-backup-retention-configure)

- storage account gen2 : life cycle management
    - tiers
    - life cycle management policies
    - immutablity
    - legal hold using tags
- azure sql backup:
    - PITR / Long Term
    - temporal tables (too much)
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

## [design to purge data based on business requirements](#data-purge)
- storage account
    - life cycle management
    - immutablity
    - legal hold using tags
- azure sql db
    -
## [design Azure role-based access control (Azure RBAC) and POSIX-like Access Control List (ACL) for Data Lake Storage Gen2](#rabc-acl)

- Reference 
    - [Access control model in Azure Data Lake Storage Gen2](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-access-control-model)
    - [Access control lists (ACLs) in Azure Data Lake Storage Gen2](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-access-control)
- Model
    - Shared Key : no identity
    - SAS Token : no identity
    - RBAC : identity based, course grain. ACL are ignored if identity has access
    - ACL  : identity based, fine grain. ACL are considered if RBAC does not provide the necessary permissions for the operation
        - Access ACL : applied to an object. file or folder
        - Default ACL : template for a folder. applied to child items
        - permissions are stored on item. they are not inherited
        - permissions are inherited from parent if
            - default permissions are set on parent
            - default permissions are set before child is created
        - common scenarios for operation
            - READ FILE     : X on folder heirarchy. R on file
            - UPDATE FILE   : X on folder heirarchy. RW on file
            - DELETE FILE   : X on folder heirarchy. WX parent folder
            - CREATE FILE   : X on folder heirarchy. WX parent folder
            - LIST DIRECTORY: X on folder heirarchy. RX on folder
        - associations
            - owner user 
            - owner group
            - named user
            - named group
            - service principal
            - managed identities
            - rest of users
    - mask : when new child is created
        - owner user : rwx|rw- 
        - owner group: r-x|r--
        - rest       : ---|---
    - unmask: when new child is created
        - default
            - copies default ACL for owner user
            - copies default ACL for owner group
            - no access for rest of the users 
        - if default ACL is defined for parent. copies it to the new child
    - sticky bit : allows only the owner user to delete / rename files.

## [design row-level and column-level security 🔒](#row-column-security)
- azure synapse | azure sql db
    - row level security using predicte
        - create separate schema 
        - create predicate table valued function
        - create security policy : assigns tvf to a table
        - grant select access on tvf for the user
    - column level security : grant access to the user
        - user gets error when projecting columns that don't fall in the grant scope