# Add a new source table in existing replication process

This section provides instructions on how to add a new table from the source database to an existing replication process. 

The procedure ensures that the table is incorporated without interrupting any ongoing replication activities or associated services. The serverconfig utility will be used to facilitate the addition of the new table to the replication configuration. 


Below process user required to be follow to add a new table at source :

1.	Then run serverconfig with below command :

```ruby
./ serverconfig  -addtabletopub -s <path_to_publication.config> -sub <path_to_subscription.config> -tables <comma_separated_table_list>
```
 
<!-- <div style="text-align: center;"> <img src="../images\image3.png" alt="addtabletopub command image"> </div> -->

That’s all. The table will be added to the replication process.

> [!Note]
> Replication for the newly added table will remain inactive until data is inserted into the table by application. In other words, the replication process does not begin for the new table until it contains at least one row of data. To initiate replication for this table, ensure that data is inserted after it has been added to the replication configuration. This behavior is by design and helps prevent unnecessary replication activity for empty tables.

## To create adhoc snapshot for a table already in replication

An adhoc snapshot may be required to synchronize __historical__ data for specific tables within the replication environment. This process is particularly useful when discrepancies are identified in the historical data between the source and target tables.

By executing an adhoc snapshot, the affected table can be synchronized with the source, ensuring data consistency while allowing the replication process to continue uninterrupted. The adhoc snapshot operation does not interfere with the ongoing replication activities, nor does it introduce any risk of data inconsistency. This functionality is designed to provide users with an efficient method for correcting historical data mismatches without impacting the performance or integrity of the replication system.

To create an __adhoc snapshot__ run the following command :

```ruby
./serverconfig  -adhocsnapshot -s publication.config -tables scott.table1,scott.table2,helyx.table1
```

  

>[!Note]
> When specifying multiple table names in a comma-separated list, ensure that there are no spaces between the table names and commas.


---

### ⬅️ Previous Page

[Configure Subscription Service](/docs/subscription.md)