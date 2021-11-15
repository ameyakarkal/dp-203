# Sovereignity

## Ownership of data
- where is data stored | data is subject to laws / rules of the country where the data is collected from
- microsoft trust center


## azure policies
1. resources can be created
2. data can be replicated
   - LRS  (three replicas in same zone)
   - ZRS  (three replicas in same region across three zones)
   - GZRS (three replicas in same zone, one replica in geo sync zone)
3. SQL replication : active read geo replication | a new sql database instance needs to be provisioned in the new replication region
4. storage account replication : geo replication can be stopped at any time
5. virtual machine : geo replication enabled
   
