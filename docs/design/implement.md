# Implement physical data storage structures

## [implement data compresion](#implement-data-compress)
- Reference : 
    - [docs : Data Compression](https://docs.microsoft.com/en-us/sql/relational-databases/data-compression/data-compression?view=sql-server-ver15)
    - [docs : Data Compression - how it affects storage](https://docs.microsoft.com/en-us/sql/relational-databases/data-compression/row-compression-implementation?view=sql-server-ver15)
    - row compression :  when compressed, database engine chooses to store fixed len data types as variable len. e.g ; datetime stored as two int representing days from 1/1/1900
    - page compression
        - leaf pages : subjected to three types of compression in order
            - row compression 
            - prefix compression : 
                - prefix entry made as a row
                - for column value is replaced by reference to the prefix
                - it also specifies if exact or partial match
            - dictionary compression :
        - non leaf pages
            - subjected to row level compression
        - it is triggered when data is added to the table and the page gets full. when new data is added to the  table and the row cannot fit onto the page after compression, a new page is created
        - when compression is added to an existing table, each page is evaluated and rebuilt
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
