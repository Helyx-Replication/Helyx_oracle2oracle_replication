# SetUp Helyx Replication services

Setting up Helyx replication services is a simple and efficient process. To initiate replication services, execute the configuration service executables as described below :

## 1. Starting helyx-sync-manager

Execute the following command to start the sync manager :

```ruby
./configservice -start helyx-sync-manager -datapath <phycal path for helyx-sync-manager>
```

The datapath specifies the directory location on your virtual machine (VM) or physical server. 

Ensure this directory is created prior to running the above command :

```ruby
mkdir -p <your datapath location>
```

> [!NOTE]
> Keep at least 20GB of storage at the datapath 

Create config directory named config at **/var/lib/helyx** location. This path is related to configpath parameter.

Place all required properties and configuration files :

+ helyx-broker-manager.properties
+ helyx-schema-registry-manager.properties
+ helyx-connect-service-manager.properties
+ publication.config
+ tablelist.config
+ subscription.config

under the **/var/lib/helyx/config** directory.


## 2. Starting helyx-broker-manager

To launch the broker manager, use the command :

```ruby
./configservice -start helyx-broker-manager -datapath <phycal path for helyx broker-manager> -configpath /var/lib/helyx/config/helyx-broker-manager.properties
```

Ensure the **datapath** directory exists on your VM or physical server before executing the above command. **helyx-broker-manager** datapath must be different from **helyx-sync manager**.

> [!Note]
> Keep at least 50GB of storage at the helyx broker-manager datapath


## 3. Starting helyx-schema-registry-manager

Start the schema registry manager with the command :

```ruby
./configservice -start helyx-schema-registry-manager -configpath /var/lib/helyx/config/helyx-schema-registry-manager.properties
```

> [!Note]
> The specified configpath must exist on your VM or physical server.
> otherwise, the program will return to an error.


## 4. Starting helyx-connect-service-manager

Start the connect service manager with the command :

```ruby
./configservice -start helyx-connect-service-manager -configpath /var/lib/helyx/config/ helyx-connect-service-manager.properties
```

## 5. To get all commands type HELP

```ruby
./configservice -help
```

---

### ⬅️ Previous Page

[Generate and Install Helyx License Certificate](/docs/generate-license.md)  

### Next Page ➡️

[Configure Publication Service](/docs/publication.md)