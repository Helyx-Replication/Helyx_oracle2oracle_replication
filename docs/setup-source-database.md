
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

## Operating System Requirements

+ Operating System: Linux (RHEL, CentOS, Rocky Linux, Oracle Linux, Fedora)
+ Privileges: Root or sudo access
+ Package Manager: yum or dnf
+ Network Access: Access to configured YUM repository


---  

### Next Page ➡️

[SetUp Destination database](docs/setup-destination-database.md)