# Design a data storage structure
Reference : https://www.youtube.com/playlist?list=PL-oeM7CaGtVjRgNJ5oy9xbrpcOYr3RhZG

##  design an Azure Data Lake solution
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
        - 

## recommend file types for storage
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


- [ ] recommend file types for analytical queries
- [ ] design for efficient querying
- [ ] design for data pruning
- [ ] design a folder structure that represents the levels of data transformation
- [ ] design a distribution strategy
- [ ] design a data archiving solution