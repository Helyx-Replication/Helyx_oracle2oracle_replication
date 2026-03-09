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

## Generating and Installing Helyx License Certificate 

To ensure seamless operation of Helyx, users are required to generate a certificate.

The following process must be followed to obtain the certificate :

+ An initial certificate valid for 30 days is available free of charge.
+ After the initial 30-day period, users are required to pay the applicable licensing fee to generate a new certificate valid for 365 days.

#### Please follow the outlined steps to complete the certificate generation process :

### 1. Extract the Certificate Utility

After downloading the Helyx zip file, extract its contents. The certificate utility **helyx-license** executable will be included in the extracted files.

### 2. Run the Certificate Utility

Execute the certificate utility. Upon running, it will display your Activation Key.

### 3. Save Your Activation Key

Copy the Activation key and keep it in a secure location. You will need this for license generation.

### 4. Access the License Portal

Go to - [Helyx replication official website](https://helyx.quobotic.com/) and log in using your registered email and password.

### 5. Generate the License File

1.	Enter the Activation Key obtained from step 2.
2.	Select the product type as prompted.
3.	Choose the appropriate license option timeline.
4.	Click to generate the license file.

### 6. Download and Install the License

1. Download the generated license file (provided as a zip file) to your system.
2. Transfer the downloaded file to server and Unzip license file.

### 7. Run the below command

```ruby
helyx-license --store-certificate -connectpath <path_to_unzipped_connect.crt> -keypath <path_to_unzipped_keystore.jks> -trustpath <path_to_Unzipped_truststore.jks> -capath <path_to_unzipped_ca.crt> 
```


### 8. Complete Setup

After completing these steps, Helyx is ready for use with a valid license.

 

## Check license validity:

You can check your license validity using the command below:

```ruby
./helyx-license --check-license-validity
```


## Setting Up Helyx Replication services

Setting up Helyx replication services is a simple and efficient process. To initiate replication services, execute the configuration service executables as described below :

### 1. Starting helyx-sync-manager

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


### 2. Starting helyx-broker-manager

To launch the broker manager, use the command :

```ruby
./configservice -start helyx-broker-manager -datapath <phycal path for helyx broker-manager> -configpath /var/lib/helyx/config/helyx-broker-manager.properties
```

Ensure the **datapath** directory exists on your VM or physical server before executing the above command. **helyx-broker-manager** datapath must be different from **helyx-sync manager**.

> [!Note]
> Keep at least 50GB of storage at the helyx broker-manager datapath


### 3. Starting helyx-schema-registry-manager

Start the schema registry manager with the command :

```ruby
./configservice -start helyx-schema-registry-manager -configpath /var/lib/helyx/config/helyx-schema-registry-manager.properties
```

> [!Note]
> The specified configpath must exist on your VM or physical server.
> otherwise, the program will return to an error.


### 4. Starting helyx-connect-service-manager

Start the connect service manager with the command :

```ruby
./configservice -start helyx-connect-service-manager -configpath /var/lib/helyx/config/ helyx-connect-service-manager.properties
```

### 5. To get all commands type HELP

```ruby
./configservice -help
```

---

### ⬅️ Previous Page

[SetUp Destination database](/docs/setup-destination-database.md)  

### Next Page ➡️

[Configure Publication Service](/docs/publication.md)
