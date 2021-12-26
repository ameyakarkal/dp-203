 # azure databricks
Reference : 
- [youtube](https://www.youtube.com/watch?v=32Jw0F5ojcU)
- [youtube](https://youtu.be/igNxBi3tfWk?list=PL7ZG6NdDdT8NRHDU5shVgGjlua297bm-H)
- benefit
    - rbac
- workspace 
    - concept
        - in a subscription
        - in a region
        - has a pricing tier
        - has one or more notebooks
        - data: has one or more tables
        - compute: has one or more clusters
        - has one or more jobs
    - types
        - shared workspace
        - private workspace
    - spark         : workflow
    - sql analytics : post workflow serving layer for visualization
- clusters
    - under the hood, its a managed cluster running apache spark.
    - run notebooks, jobs.
    - max timeout
    - auto scale with min and max node counts
    - consists of two types of nodes
        - driver (jobmanager for flink)
        - worker (taskmanager for flink)
    - types
        - interactive: 
            - manual start/stop/reused
            - life cycle is independent of a job (notebook / job)
            - auto pause
            -  no 
            - types
                - standard mode : single user, no fault toleration, not fair sharing 
                - high concurrency mode : multi user, fault toleration, limited support for languages, fair sharing
        - job cluster : associated with a job
            - deleted with the job
        - single node cluster
    - scheduler : 
        - determines jobs access to cluster
        - uses preemption
        - threshold settings between 0-1.
        - preemption timeout : time for which a job can starve for job before preemption
        - interval : time interval between two checks done by schedule to check if a job needs resources

    - pool
        - nodes available which can be added to a cluster
        - cluster requests nodes from the pool, if not available will spin up new nodes
        - nodes from the pool can be shared by cluster. reduces time to wait on nodes
    - initialization scripts
        - global
        - cluster scoped
    - node types (not given)
        - on demand
        - spot (node is terminated as soon as the task is complete, disk attached to the node are released as well)
- notebooks
    - mutliple code cells
    - unlimited code cells
    - cell
        - single language
        - versioned
        - limit of 16 mb +  output
    - dataframe to table
    - dataframe to plots
    - publish notebook to dashboards and share dashboard
    - dashboard are not real time, set a schedule to refresh them
- jobs
    - jobs are non interactive compared to notebook
    - artifact created : jobrun
    - job cluster : 
        - new cluster : isolated environment to run job tasks
        - existing cluster
    - alerts :  notification when job starts/stops/fails/completes/skips
    - tasks:
        -libraries
    - limits 
        - 5000 per workspace per hour
        - 1000 jobs concurrently
        - maximum job output of 20 mb
        - cell output limit of 8 mb
    - configuration:
        - manual : triggered by user
        - scheduled : cron style setup
        - task 
            - work : pick notebook to be run
            - cluster : create new cluster/pick existing cluster
            - params : key/value pairs
    - disk space
        - local storage used by VM
        - when exceeded local storage, managed disks are added to the VM
        - 5TB limit
    - streaming job
        - limits
            - no schedule
            - unlimited retries
            - single concurrent run
        - watermarks : defines accepted time delay for event to be included in a window
            - 1 min aggregate with 2 min watermark will include events that are 2 min delayed. the aggregate will be calculated every 2 minutes (instead of every minute)
            - if two streams are joined the global watermark will be the highest (1 hr stream joined with 2 hr stream, the output stream will have a 2 hr watermark) 
- data
    - can connect to azure services
    - it has a internal file system
    - mount account storage 

```bash
source="wasbs://<container_name>@<account_name>.blob.core.windows.net"
mount_point="/mnt/<mount_name>"
conf_key="fs.azure.account.key.<account_name>.blob.core.windows.net"
key_name="<storage_account_shared_access_key>"


# mount account storage using
dbutils.fs.unmount(mount_point)
dbutils.fs.mount(source = source, mount_point, extra_config = {conf_key:key_name})
```