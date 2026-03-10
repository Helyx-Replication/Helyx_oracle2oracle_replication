# SetUp Docker env for Helyx Replication

To facilitate the setup and execution of replication between Oracle databases, users are required to download a **zip** file.

This package contains five executable files : 

+ configservice
+ serverconfig
+ MetaSync
+ tabletorepl
+ helyx-license

Additionally, it includes essential configuration files such as :

+ helyx-broker-manager.properties
+ helyx-schema-registry-manager.properties
+ helyx-connect-service-manager.properties
+ publication.config
+ tablelist.config
+ subscription.config 

which are necessary for proper configuration and operation of the replication services.

## Installation of Docker software

To install Docker and configure the necessary repository on your system, execute the following commands with **root** or **sudo privileges** [ For **Linux environment** ] :

### 1. Install the yum-utils package

```ruby
sudo dnf install -y yum-utils
```

### 2. Add the Docker repository

```ruby
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```

### 3. Install Docker Engine and related components

```ruby
sudo dnf install -y docker-ce docker-ce-cli containerd.io
```

### 4. Enable the Docker service to start on boot

```ruby
sudo systemctl enable docker
```

### 5. Start the Docker service

```ruby
sudo systemctl start docker
```

### 6. Verify the Docker installation

```ruby
docker –version
```


For __Ubuntu__ based system use __apt-get__ command.




## Docker Installation on Ubuntu

Follow the steps below to install __Docker Engine__ and related components on an __Ubuntu-based__ system :

### Update the Package Index. 

1. Run the following command to ensure your package index is up to date :

```ruby
sudo apt update
```

2. Install Required Packages for necessary certificates, tools, and libraries :

```ruby
sudo apt install ca-certificates curl gnupg lsb-release -y
```
3. Add Docker's GPG Key and Create the keyrings directory and add Docker’s official GPG key :

```ruby
sudo mkdir -p /etc/apt/keyrings
```

```ruby
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

4. Set Up the Docker Repository and add Docker’s repository to your sources list :

```ruby
echo \
"deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

5. Update the Package Index again and refresh the package index to include the Docker repository :

```ruby
sudo apt update
```

6. Install Docker Components like Docker Engine, CLI, containerd, Buildx plugin, and Compose plugin :

```ruby
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
```

7. Verify Docker Installation

```ruby
docker –version
```

These steps will ensure Docker is installed and operational on your Ubuntu system.

These steps ensure that Docker is properly installed and operational on your Linux as well as **Ubuntu system**, which is required for the Helyx replication setup.


---

### ⬅️ Previous Page

[SetUp Destination database](/docs/setup-destination-database.md)  

### Next Page ➡️

[Generate and Install Helyx License Certificate](docs/generate-license.md)
