## alerting

- actions
    - dashboard
    - email
    - sms
    - itsm
    - automation / webhook
- action groups
    - triggered by alert group
- sources
    - metrics (sinks : azure monitor)
        - types : cpu | memory | dtu / wu
        - sink  : azure monitor
    - activity log (sinks : azure monitor)
        - crud on resource
        - changes on the azure resource fabric level
    - diagnostics (sinks : log analytics workspace | event hub | storage account)
        - event hub / storage account need to sink to azure monitor logs(log analytics)
    - service health (sinks : service health)
    - cost management
        - currently do not use action groups
        - currently do not use azure monitor

- alerts
    - alerts on azure monitor
        - you can separate out alerting from the actual action.
            - define an alert without an action to be taken
            - define action rule
            - this helps to setup a single action on multiple types / alerts on multiple type of resources
    - alerts on service health
        - alerts on service health / maintenance
    - alerts on azure monitor (log analytics) logs
        - similar to alerts on azure monitor logs but are priced differently

# monitoring per service
## storage
- metrics       : goes into azure monitor
- activity log  : goes into azure monitor
- diagnostics   : uses classic diagnostics
    - sinks to $log folder of a blob container
    - blob container then can be made visible into azure monitor

## azure sql database
- metrics       : goes into azure monitor
- activity log  : goes into azure monitor
- diagnostics   : goes into log analytics workspace and available in azure monitor

# azure cosmo DB
- metrics       : goes into azure monitor
- activity log  : goes into azure monitor
- diagnostics   : goes into log analytics workspace and available in azure monitor

# azure data factory
- metrics       : goes into azure monitor
- activity log  : goes into azure monitor
- diagnostics   : goes into log analytics workspace and available in azure monitor

# azure HD insight
- metrics | activity log : goes into azure monitor
- ambari setup

:::mermaid
    flowchart LR

    %% PARTICIPANTS: sourcs
    METRICS[metrics]
    ACTIVITY_LOG[activity log]
    DIAGNOSTICS[diagnostics]

    %% PARTICIPANTS : sink
    AZURE_MONITOR[azure monitor]
    LOG_ANALYTICS[log analytics]
    EVENT_HUB(event hub)
    STORAGE_ACCOUNT(storage account)

    METRICS --> AZURE_MONITOR
    ACTIVITY_LOG --> LOG_ANALYTICS


    DIAGNOSTICS -->LOG_ANALYTICS
    DIAGNOSTICS --> EVENT_HUB
    DIAGNOSTICS --> STORAGE_ACCOUNT
:::