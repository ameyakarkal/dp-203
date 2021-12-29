# Azure Stream Analytics

Reference 
- [Azure Stream Analytics](https://www.youtube.com/watch?v=AVNu5EGwnTU&list=PL7ZG6NdDdT8NRHDU5shVgGjlua297bm-H&index=9)

Implementation
- HDInsight Spark Stream
- HDInsight Storm
- Apache Spark in Databricks
- Azure Stream Analytics

Concept
- Job
    - Streaming Units : handles scaling
    - Inputs
    - Query
    - Functions
    - Outputs
- Event Ordering : specify actions to take for late arriving events
## Windowing
### tumbling window : 
- unit of measure
- unit of time
```sql
/*
    captures events in intervals of 10 seconds
*/
select count(*), tenantId
FROM TenantStream
GROUP BY tenantId, TumblingWindow
(
    second, /*unit of measure*/
    10      /*time range for the window*/
)
```
### hopping window

```sql
select count(*), tenantId
FROM TenantStream
GROUP BY 
    tenantId, 
    HoppingWindow
    (
        second, /*unit of measure*/
        10,     /*time range for the window*/
        5       /*time range to consider before the window starts, defines the overlap with the previous window*/
    )
```
- window 01 : starts at 0, ends at 10
- window 02 : starts at 5, ends at 15
- window 03 : starts at 15, ends at 20
- always overlapping

### sliding window
```sql
select count(*), tenantId
FROM TenantStream
GROUP BY 
    tenantId, 
    SlidingWindow
    (
        second, /*unit of measure*/
        10,     /*time range for the window*/        
    )
```
- depends on the event that was captured
- overlap may or may not occur
- alerts when event enters or exists the window
- goes back 10 seconds from each event that is captured

### session
```sql
select count(*), tenantId
FROM TenantStream
GROUP BY 
    tenantId, 
    SessionWindow
    (
        second, /*unit of measure*/
        5,     /* no event timeout*/
        10       /*time range to consider before the window starts, defines the overlap with the previous window*/
    )
```
- windows starts with event captured
- window terminates if no new events are captured in 5 minutes
- window terminates time span divisible by 10 (10,20,30)

## Demo
- define input 
    - event hub
    - iot
    - blob
- define output
- define job queryer
    - manual or scheduled
    - defined number of rows generated / max timespan the job needs to run
- monitoring
    - watermark delay : time taken by event to be consumed and processed to be available at the destination
- optimization
    - use partitioning key for parallelization
    - event hub specified partition is ideal 