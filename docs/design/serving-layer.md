# serving layer
- fact : more rigid structure
- dimensions : flexible
- hierarchy : levels of data formed


## [serving using parquet](#parquet)
- Reference : [youtube: parquet](https://www.youtube.com/watch?v=1j8SdS7s_NY&list=RDCMUC3q8O3Bh2Le8Rj1-Q-_UUbA&index=8)
- row-wise      : good for OLTP : rows are stored back to back
- column-wise   : good for OLAP : columns are stored back to back
- hybrid        : columns are stored and rows are stored back to back in groups

parquet
- structure
    - ROW GROUP -> COLUMN CHUNK 
    - file has multiple row groups
    - row groups : 128 MB
        - row groups has multiple column chunk
        - column chunk : min, max values, statistics        
    - footer : metadata for the row
- optimization
    - increase dictionary size
    - decrease row group size
    - page  
- encoding 
    - plain
        - fixed length rows
    - dictionary 
        - one dictionary per column chunk
        - figure out statistics
        - organize by dictionary
        - bit packing

- delta lake
    - OPTIMIZE : run on files
    - zordering
