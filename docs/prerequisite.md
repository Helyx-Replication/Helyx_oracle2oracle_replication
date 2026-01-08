# Pre-requisites for Source Database

### Source Database in ARCHIVELOG Mode
The source Oracle database must operate in ARCHIVELOG mode. Helyx relies on archived redo logs to capture transactional changes reliably.

### Enable Supplemental Logging
Supplemental logging is mandatory to ensure complete row-level data is available for replication.

```ruby
SQL> ALTER DATABASE ADD SUPPLEMENTAL LOG DATA;
```

### Create Helyx User at Source Database
Create a dedicated database user for Helyx replication activities.
```ruby
SQL> CREATE USER helyx IDENTIFIED BY <password>;
```

### Grant Required Privileges
Grant the following privileges to the helyx user:

```ruby
SQL> GRANT CONNECT, RESOURCE TO helyx;
```
```ruby
SQL> ALTER USER helyx QUOTA UNLIMITED ON USERS;
```
```ruby
SQL> GRANT UNLIMITED TABLESPACE TO helyx;
```

> [!NOTE]
> By default, Helyx creates objects in the USERS tablespace. If a different tablespace is required, create the user as shown below.

Example:
```ruby
SQL> CREATE USER helyx IDENTIFIED BY <password> DEFAULT TABLESPACE tblspc_helyx QUOTA UNLIMITED ON tblspc_helyx;
```
### Create Debezium Signal Table
The Debezium signal table is required for snapshot control and runtime signaling.

```ruby
SQL> CREATE TABLE helyx.debezium_signal (
  id   VARCHAR2(42) PRIMARY KEY,
  type VARCHAR2(32) NOT NULL,
  data VARCHAR2(400)
);
```
```ruby
SQL> GRANT SELECT, INSERT, UPDATE, DELETE ON HELYX.DEBEZIUM_SIGNAL TO helyx;
```

### Operating System Requirements
+ Operating System: Linux (RHEL, CentOS, Rocky Linux, Oracle Linux, Fedora)
+ Privileges: Root or sudo access
+ Package Manager: yum or dnf
+ Network Access: Access to configured YUM repository
