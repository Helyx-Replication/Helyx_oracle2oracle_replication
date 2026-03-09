
# SetUp Destination database


## 1. Create a dedicated database user at destination database for Helyx replication activities.

```ruby
CREATE USER helyx IDENTIFIED BY <password>;
```
 
> [!Note]
> The password for helyx user at source and destination database must be same.


## 2. Grant Required Privileges

Grant the following privileges to the helyx user :

```ruby
GRANT CONNECT, RESOURCE TO helyx;
```

```ruby
ALTER USER helyx QUOTA UNLIMITED ON USERS; 
```

```ruby
GRANT UNLIMITED TABLESPACE TO helyx;
```


> [!Note]
> By default, Helyx creates objects in the USERS tablespace.

If a different tablespace is required, create helyx user as shown below.

```ruby
CREATE USER helyx IDENTIFIED BY <password> DEFAULT TABLESPACE tblspc_helyx QUOTA UNLIMITED ON tblspc_helyx;
```


## 3. Provide necessary privileges to helyx user at destination database

```ruby
GRANT	SELECT	ANY	TABLE	TO	HELYX;
```

```ruby
GRANT	INSERT	ANY	TABLE	TO	HELYX;
```

```ruby
GRANT	UPDATE	ANY	TABLE	TO	HELYX;
```

```ruby
GRANT	DELETE	ANY	TABLE	TO	HELYX;
```

```ruby
GRANT	CREATE	ANY	TABLE	TO	HELYX;
```

```ruby
GRANT ALTER ANY TABLE TO HELYX;
```

```ruby
GRANT CREATE ANY INDEX TO HELYX; 
```

```ruby
GRANT CREATE ANY TRIGGER TO HELYX;
```


---

### ⬅️ Previous Page

[Setup Source Database](setup-source-database.md)  

### Next Page ➡️

[SetUp Docker env for Helyx Replication](docker-env-setup.md)
