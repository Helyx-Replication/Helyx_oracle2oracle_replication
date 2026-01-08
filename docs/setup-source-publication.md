# Setting Up Source Publications

### Start Sync-Manager Service
```ruby
./configservice -start sync-manager
```
### Start Broker Service
Edit __/var/lib/helyx/server.properties__ and set:
```ruby
listeners = PLAINTEXT://your.host.name:9092
```
```ruby
./configservice -start broker
```

### Start Schema Registry Service
Edit __schema-registry.properties__ and configure:
```ruby
kafkastore.bootstrap.servers=PLAINTEXT://<your.host.name>:9092
```

listeners=http://0.0.0.0:8081
```ruby
./configservice -start schemaregistry
```

## Start Connect Service
Edit __connect-distributed.properties__ and set:
```ruby
bootstrap.servers=<your.server.ip>:9092
```
```ruby
key.converter.schema.registry.url=http://<your.server.ip>:8081
```
```ruby
value.converter.schema.registry.url=http://<your.server.ip>:8081
```
```ruby
./connectservice -start connect
```

### Configure publication.config
Edit __/var/lib/helyx/replconfig/publication.config__ and set all required parameters exactly as documented.

### Configure Table List
```
Schema1.Table1,
Schema2.Table2,
Schema2.Table3
```
```ruby
./tabletorepl.jar -s <path_to_publication.config> -tables <path_to_tablelist.config>
```

### Start Publication
```ruby
serverconfig -createpub -s publication.config -tables tablelist.config
```
