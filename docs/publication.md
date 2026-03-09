# Configure publication.config

Edit __/var/lib/helyx/replconfig/publication.config__ and set all required parameters.

|Parameter | Description | Purpose | Example |
|----------|-------------|---------|---------|
|name |Unique name of the source connector.|Used to identify and manage the connector instance.| oracle-source-connector |
|tasks.max | Maximum number of tasks the connector can run. | Controls the level of parallel processing for the connector. | 1 |
|bootstrap.ip	|IP address of the Helyx physical server or VM.	|Allows the connector to connect to the helyx-broker-manager for publishing change events.	|192.xxx.xxx.xxx|
|database.server.name|	Logical name of the oracle source database server.	|Used as a namespace for topic generation and database identification.	|ORCLSRC|
|database.hostname|	Hostname or IP address of the source database.	|Used by the connector to connect to the oracle  source database server.	|192.xxx.xxx.xxx|
|topic.prefix|	Prefix used when creating topics for captured tables.|	Helps organize topics related to this connector.	|oraclecdc|
|database.port|	Port number used to connect to the source database.	|Required for establishing database connectivity.|	1521|
|database.password	|Password of the database replication user[helyx].|	Used for authentication with the source database.	|********|
|database.dbname|	Name of the source database instance.	|Specifies which database the connector should capture changes from.	|ORCLCDB|
|log.mining.archive.destination|
Archive log destination used for Oracle LogMiner.	|Allows the connector to read archived redo logs for change capture.|	LOG_ARCHIVE_DEST_1|
|schema.history.internal.kafka.topic|	Helyx topic used to store schema history.|	Maintains database schema changes for proper event processing.|	schema-changes-oracle|
|schema.history.internal.kafka.recovery.poll.interval.ms|	Polling interval for recovering schema history.	|Helps the connector retrieve schema history during restart or recovery.	|500|
|poll.interval.ms|	Time interval for polling database changes.|	Determines how frequently the connector checks for new change events.|	50|
|topic.creation.default.min.insync.replicas|	Minimum number of in-sync replicas for topics.	|Ensures data reliability when writing messages to topics.|	1|
|topic.creation.default.partitions|	Default number of partitions for topics.	|Controls parallelism and distribution of data across brokers.|	1|
|topic.creation.default.replication.factor|	Number of replicas maintained for each topic.|	Provides fault tolerance and data redundancy.|	1|
|heartbeat.interval.ms|	Interval at which heartbeat messages are sent.|	Helps monitor connector health and connectivity.|	10000|
|log.mining.batch.size.default	|Default batch size for LogMiner processing.|	Defines how many redo log records are processed in one batch.	|500|
|database.connection.timeout.ms|	Maximum time allowed for database connection attempts.|	Prevents long waits if the database connection fails.|	30000|
|batch.size|	Number of events processed in a single batch.|	Improves performance by processing multiple records together.|	65536|
|max.batch.size|	Maximum number of records returned in a batch.	|Controls processing limits and memory usage.|	1000|
|max.queue.size	|Maximum number of records allowed in the internal queue.	|Buffers events before they are processed by the connector.|	10000|
|lob.chunk.size	|Size of chunks used for LOB (BLOB/CLOB) data processing.	|Helps efficiently process large object data types.|	8192|
|log.mining.batch.size.max|	Maximum batch size for LogMiner processing.|	Limits the maximum number of redo log entries processed per batch.|	10000|


## 1. Configure tablelist.config

Users are required to specify a list of table names within the configuration files named tablelist.config. These tables are part of the replication pipeline and will be replicated to the target database.

The table list should be provided as __comma-separated__ values, each including the fully qualified schema name. For example, if table1 resides in the scott schema, the entry should be formatted as __scott.table1__. If table2 resides in helyx schema, the entry should be formatted as __scott.table1__, __helyx.table2__.


## 2. Metasync

The Metasync process is designed to gather and construct comprehensive metadata for database tables, ensuring accurate and efficient data management.

It is essential to execute the Metasync utility once prior to initiating the publication service for the source database. This preliminary step establishes the necessary metadata foundation, enabling smooth operation and replication within the database environment.


Run the below command :

```ruby
./MetaSync -s <fully_qualified_path_to_publication.config>
```

Metasync will ask for __SYS user id__ and __password__ for source database.

For example:

### To get command help run below :

```ruby
./MetaSync -help
```


## 3. tabletorepl 

This procedure grants the necessary privileges to the helyx user, ensuring seamless replication between the source and target databases.

Assigning the appropriate permissions is critical because, without them, the helyx replication process may encounter errors or experience interruptions, potentially impacting the integrity and consistency of the replicated data. By providing the required access rights from the outset, you help guarantee that the replication workflow operates smoothly and reliably throughout the system. 

User required source database __sys user__ and __sysdba__ privileges to run the command below : 

```ruby
./tabletorepl -s <full_qualified_path_to_publication.config> -tables <full_qualified_path_to_tablelist.config>
```

### To get command help run below

```ruby
./tabletorepl -help
```

For example :

<div style="text-align: center;"> <img src="../images\image2.png" alt="tabletorepl image"> </div>


## Start Publication Service

### serverconfig

This program is essential components required to initiate and manage both the __publication__ and __subscription__ services within the replication framework. These executables facilitate seamless data replication between source and target databases, ensuring __operational reliability__ and __data consistency__ throughout the replication process.

Proper configuration and execution of these executables are fundamental to establishing, maintaining, and monitoring replication workflows in accordance with system requirements and best practices.
 
#### To start Publication service

```ruby
./serverconfig -createpub -s publication.config -tables tablelist.config
```

---

### ⬅️ Previous Page

[SetUp Docker env for Helyx Replication](docker-env-setup.md)  

### Next Page ➡️

[Configure Subscription Service](docs/subscription.md)