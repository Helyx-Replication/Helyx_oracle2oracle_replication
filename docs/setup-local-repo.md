# Setting Up Local Repository for Helyx Installation

### Create Local Repository Directory
```ruby
mkdir -p /opt/localrepo/helyx
```

### Copy Helyx RPM Package
```ruby
cp helyx-1.1.0.rpm /opt/localrepo/helyx/
```

### Create Repository Metadata
```ruby
cd /opt/localrepo/helyx
```
```ruby
createrepo .
```
> [!NOTE]
> Install createrepo before executing this step.

### Configure Local YUM Repository
Create __/etc/yum.repos.d/helyx-local.repo__ with the following content:
```ruby
[helyx-local]
name=Helyx Local Repository
baseurl=file:///opt/localrepo/helyx
enabled=1
gpgcheck=0
```
### Install Helyx
```ruby
sudo yum install helyx -y
```

### Target
Establish real-time replication between Oracle source and Oracle destination databases (same or different Oracle versions).
