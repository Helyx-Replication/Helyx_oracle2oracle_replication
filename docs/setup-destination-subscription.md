# Setting Up Destination Subscription

### Create Helyx User on Destination Database
```ruby
SQL> CREATE USER helyx IDENTIFIED BY <password>;
```
### Grant Required Privileges
```ruby
SQL> GRANT CONNECT, RESOURCE TO helyx;
```
```ruby
SQL> ALTER USER helyx QUOTA UNLIMITED ON USERS;
```
```ruby
SQL> GRANT UNLIMITED TABLESPACE TO helyx;
```
```ruby
SQL> GRANT SELECT ANY TABLE TO HELYX;
```
```ruby
SQL> GRANT INSERT ANY TABLE TO HELYX;
```
```ruby
SQL> GRANT UPDATE ANY TABLE TO HELYX;
```
```ruby
SQL> GRANT DELETE ANY TABLE TO HELYX;
```
```ruby
SQL> GRANT CREATE ANY TABLE TO HELYX;
```
```ruby
SQL> GRANT ALTER ANY TABLE TO HELYX;
```
```ruby
SQL> GRANT CREATE ANY INDEX TO HELYX;
```
```ruby
SQL> GRANT CREATE ANY TRIGGER TO HELYX;
```

### Configure subscription.config
Edit __/var/lib/helyx/replconfig/subscription.config__ with destination database details and replication parameters.

### Start Subscription
```ruby
serverconfig -createsub -s subscription.config -pub publication.config
```
### Verify Status
```ruby
serverconfig -status -pub -s publication.config
```
```ruby
serverconfig -status -sub -s subscription.config
```