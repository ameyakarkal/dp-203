# Implement physical data storage structures

## implement data archiving
- azure sql : rentention
    - Reference : [docs](https://docs.microsoft.com/en-us/azure/azure-sql/database/long-term-retention-overview)
    - PITR
        - 7 days to 35 days
        - automatically backed up sql db
    - LTR
        - Weekly|Monthly|Yearly|WeekOfYear
        - W = 12, M = 3, Y = 10 WOY = 4
            - weekly backup kept for 12 weeks
            - first monthly backup kept for 3 months
            - weekly backup taken in the 4th week kept for 10 years
- azure sql : temporal
    - Reference : [docs](https://docs.microsoft.com/en-us/azure/azure-sql/database/temporal-tables-retention-policy)
    - enable feature for database
```sql
ALTER DATABASE [<myDB>]
SET TEMPORAL_HISTORY_RETENTION  ON
```
    - enable for table
```sql
CREATE TABLE dbo.WebsiteUserInfo
(  
    [UserID] int NOT NULL PRIMARY KEY CLUSTERED
  , [UserName] nvarchar(100) NOT NULL
  , [PagesVisited] int NOT NULL
  , [ValidFrom] datetime2 (0) GENERATED ALWAYS AS ROW START
  , [ValidTo] datetime2 (0) GENERATED ALWAYS AS ROW END
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
 )  
 WITH
 (
     SYSTEM_VERSIONING = ON
     (
        HISTORY_TABLE = dbo.WebsiteUserInfoHistory,
        HISTORY_RETENTION_PERIOD = 6 MONTHS
     )
 );
```
