# Monitor and Optimize Data Storage and Processing

## [monitor data pipeline performance](#monitor)
- Reference
    - [youtube : How to monitor and optimize big data pipelines and workflows](https://www.youtube.com/watch?v=x5t0NvUnZ7o)
- Problems
    - job failure
        - check logs
        - check cpu utilization
        - check cluster health
    - configuration issues
        - resource job 
        - size of task
        - batch size
        - memory size
        - disk size
    - scaling
    - resource contention / allocation




# Optimize and troubleshoot

## compact small files

## [handle skew in data](#skew)
1. get the partition column correct. talk to the data owner
2. repartition after reading partitioned data from blob storage (file size vary in the storage)
3. cache data frames : inmemory
4. persist data frames : caching but on storage | unpersist when done
5. boardcast small data frames. spark will auto broadcast smaller data frames
6. dynamic partition pruning : sql version of pushing down the filters down to the source
7. salting the data to avoid skews


## rewrite user defined functons

## handle data spill

## tune shuffle partitions
Reference 
    - [youtube](https://www.youtube.com/watch?v=ebbx83jPbmQ)
- 
## [find shuffling in a pipeline](#find-shuffle)

- find broadcast
- find tasks that exchange

## tune queries by using cache
- Reference 
    - [youtube: 20:12](https://youtu.be/WSplTjBKijU?t=1213)
- use kryo serializer
- too many rdd are cached
- contention for more objects
- GC occuring before task complete
- frequency of GC
- long running GC
- missed heartbeats
- parallel gc

## optimize pipelines for analytical or transactional purposes
## optimize pipeline for descriptive versus analytical workloads
- Reference 
    - [youtube : descriptive vs predictive vs prescriptive](https://www.youtube.com/watch?v=-U_xkc5HeoU)
    - [youtube : diagnostic]
    - [youtube : predictive](https://www.youtube.com/watch?v=4y6fUC56KPw)
    - [youtube : prescriptive](https://www.youtube.com/watch?v=046dYegfGrc)
- descriptive : past
- predictive : model based on past
- prescriptive : tells user what need to do
