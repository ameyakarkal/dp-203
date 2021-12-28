# Spark
> Cross cutting across multiple points in the overview section
- [youtube : cost optimization](https://www.youtube.com/watch?v=q0_j2rpFjcE)
- [yuotube : data skew](https://www.youtube.com/watch?v=WSplTjBKijU)
- job level
    - job needs to be sized correctly.
- cluster level
    - cluster need to be of the right type    
- visibility
    - identify inefficient jobs
    - understand bottlenecks

- data 
    - rdd size per partition  
    - rdd records per partition 

## interpret spark DAG
 - [Reference : youtube : read spark DAG](https://www.youtube.com/watch?v=LoFN_Q224fQ)
 - different DAG generated depending on the size of the job
 - multiple JOBS can be created for a single action
 - JOB is decomposed into STAGES. each exchange (shuffle) generates a new stage
 - STAGE is decomposed into TASKS
 - Spark performs A TASK per PARTITIONs
 - http://localhost:4040 
    - wholestagecodegen     : java code generated
    - mapPartitionsInternal : every partition is treversed and each item is processed
    - exchange              : data is shuffled between executors. need to be kept minimum
     partitions the 