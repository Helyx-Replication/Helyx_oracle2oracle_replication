# Configure subscription.config

Edit __/var/lib/helyx/config/subscription.config__ with destination database details and replication parameters.


|Parameter	|Description|	Purpose|	Example|
|-----------|-----------|----------|-----------|
|name|	Unique name assigned to the sink connector.|	Used by the system to identify and manage the connector instance.|	oracle-sink-connector|
|tasks.max|	Maximum number of tasks that the sink connector can run.|	Controls the level of parallel processing when writing data to the destination database.|	2|
|bootstrap.ip	|IP address of the Helyx physical server or VM.	| Enables the sink connector to connect to the broker and consume change events.|	192.xxx.xxx.xxx|
|connection.host|	Hostname or IP address of the destination database server.|	Used to establish the connection with the destination database.	|192.xxx.xxx.xxx|
|connection.port	|Port number of the destination database.	|Specifies the port used for connecting to the destination database.|	1521|
|connection.db	|Name of the destination database.|	Indicates which database the sink connector should write the replicated data to.|	ORCLDEST|
|connection.password	|Password of the destination database replication user [helyx].|	Used for authentication when connecting to the destination database.	|********|
|retry.backoff.ms|	Time interval between retry attempts when a failure occurs.|	Prevents continuous retry attempts by adding a delay between retries.	|1000|
|batch.size	|Number of records processed in a single batch before writing to the destination database.|	Improves performance by reducing the number of database write operations.|	5000|
|max.retries	|Maximum number of retry attempts if a write operation fails.|	Ensures the connector retries failed operations before marking them as errors.	|10|

## Start Subscription

```ruby
./serverconfig -createsub -s subscription.config -pub publication.config
```

## Verify Status of Publication & Subscription

```ruby
./serverconfig -status -pub -s publication.config
```

```ruby
./serverconfig -status -sub -s subscription.config
```

---

### ⬅️ Previous Page

[Configure Publication Service](/docs/publication.md)  

### Next Page ➡️

[Add New Table To Replication](/docs/add-new-table.md)