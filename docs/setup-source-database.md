
# Setup Source Database

## Source Database in ARCHIVELOG Mode

The source Oracle database must operate in **ARCHIVELOG** mode. Helyx relies on archived redo logs to capture transactional changes reliably.

## Docker Network

Create a Docker network with the below command :

```ruby
docker network create helyx-net
```


## Enable Supplemental Logging

Supplemental logging is mandatory to ensure complete row-level data is available for replication.

```ruby
ALTER DATABASE ADD SUPPLEMENTAL LOG DATA;
```

## Create Helyx User at Source Database

Create a dedicated database user for Helyx replication activities.

```ruby
CREATE USER helyx IDENTIFIED BY <password>;
```

## Grant Required Privileges

Grant the following privileges to the helyx user:

```ruby
GRANT CONNECT, RESOURCE TO helyx;
```

```ruby
ALTER USER helyx QUOTA UNLIMITED ON USERS;
```

```ruby
GRANT UNLIMITED TABLESPACE TO helyx;
```

> [!NOTE]
> By default, Helyx creates objects in the USERS tablespace. If a different tablespace is required, create the user as shown below.

#### Example :

```ruby
CREATE USER helyx IDENTIFIED BY <password> DEFAULT TABLESPACE tblspc_helyx QUOTA UNLIMITED ON tblspc_helyx;
```


## Create Helyx Signal Table at Source database

The Debezium signal table is required for snapshot control and runtime signaling.

```ruby
CREATE TABLE helyx.debezium_signal (
  id   VARCHAR2(42) PRIMARY KEY,
  type VARCHAR2(32) NOT NULL,
  data VARCHAR2(400)
);
```

```ruby
GRANT SELECT, INSERT, UPDATE, DELETE ON HELYX.DEBEZIUM_SIGNAL TO helyx;
```


## Configuring and Creating Export Dump for Source Oracle Database

To enable replication using Helyx, it is essential to export the schemas and tables from the __source Oracle__ database that you intend to replicate.

Follow the steps below to ensure a successful export and subsequent import at the destination host :

1.	Identify Schemas and Tables for Replication.

2.	Review the list of schemas and tables required for replication.

3.	Ensure only necessary objects are included to streamline the replication process.

4.	Create Export Backup Using Oracle Data Pump.

5.	Use Oracle Data Pump (expdp) to export the identified schemas and tables.

6.	Example command :

```ruby
expdp helyx/password@source_db schemas=SCHEMA_NAME tables=TABLE_NAME directory=EXPORT_DIR dumpfile=export_dump.dmp logfile=export_dump.log
```

7.	Verify the export completion and check the log file for errors.

8.	Transfer Export Dump to Destination Host.

9.	Securely copy the generated export dump __(.dmp)__ file to the destination server using __SCP__, __SFTP__, or another secure file transfer method.

10.	Ensure proper file permissions and integrity after transfer.

11.	Import Schema and Tables at Destination Database.

12.	On the destination Oracle database, use __Oracle Data Pump (impdp)__ to import the schema and tables.

13.	Example command :

```ruby
impdp helyx/password@destination_db schemas=SCHEMA_NAME directory=IMPORT_DIR dumpfile=export_dump.dmp logfile=import_dump.log
```

14.	Verify the import completion and review the log file for any issues.

15.	Post-Import Validation.

16.	Validate the imported schemas and tables to ensure all objects are present and correct.

17.	Confirm that the destination database is ready for Helyx replication setup.


These above steps will ensure that the required schemas and tables are properly exported from the source Oracle database, transferred, and imported into the destination host, laying the groundwork for successful replication with Helyx.


## Operating System Requirements

+ Operating System: Linux (RHEL, CentOS, Rocky Linux, Oracle Linux, Fedora)
+ Privileges: Root or sudo access
+ Package Manager: yum or dnf
+ Network Access: Access to configured YUM repository


---  

### Next Page ➡️

[SetUp Destination database](/docs/setup-destination-database.md)