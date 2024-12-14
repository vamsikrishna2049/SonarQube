# SonarQube Server Setup on Ubuntu

## Prerequisites:
1. An AWS account.
2. An EC2 instance running Ubuntu (instance type must be >= t2.small).
3. Basic knowledge of SSH, EC2, and Linux commands.

---

## Steps to Set Up SonarQube Server on Ubuntu
### Step 1: Login to AWS Management Console
- Open your web browser and navigate to the (https://aws.amazon.com/console/).
- Log in with your AWS credentials.
 
### Step 2: Create an EC2 Instance
1. From the EC2 Dashboard, click on “Launch Instance”.
2. Select an Ubuntu AMI (Amazon Machine Image).
3. Choose an instance type must be `>= t2.small` (recommended: t2.medium or higher).
4. Configure your instance settings as per your requirement.
5. Make sure to configure the Security Group to allow inbound traffic on port `9000` (for SonarQube).

### Step 3: Open Security Group for Port 9000
1. Navigate to the EC2 Dashboard > Security Groups.
2. Select the security group attached to your EC2 instance.
3. Edit inbound rules and add a custom rule to allow TCP traffic on port `9000` (SonarQube default port).

### Step 4: SSH into Your EC2 Instance
1. Once the EC2 instance is up and running, get its public IP.
2. Use SSH to connect to your EC2 instance:

### Step 5: Install Java 17 (as root user)
1. Change to the root user:
``` xml
sudo su -
```
2. Download the Java 17 RPM:
``` xml
sudo apt install openjdk-17-jre-headless -y
```

### Step 6: Download and Install SonarQube
1. Change to the /opt directory:
``` xml
cd /opt
```
2. Download the SonarQube ZIP file
``` xml
sudo wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.9.1.69595.zip
```
3. Unzip the SonarQube archive:
``` xml
sudo unzip sonarqube-9.9.1.69595.zip
```

### Step 7: Create a User for SonarQube and Set Permissions
1. Create a user for SonarQube:
``` xml
sudo useradd sonaradmin
sudo passwd sonaradmin
```

2. Create a group for SonarQube:
``` xml
sudo addgroup sonargroup
```

3. Change ownership of the SonarQube directory:
``` xml
sudo chown -R sonaradmin:sonargroup /opt/sonarqube-9.9.1.69595
```

### Step 8: Switch to SonarQube User
switch to the sonaradmin user to run SonarQube:
``` xml
su sonaradmin
```

### Step 9: Start SonarQube
1. start SonarQube using the following command:
``` xml
sh /opt/sonarqube-9.9.1.69595/bin/linux-x86-64/sonar.sh start
```

2. status SonarQube using the following command:
``` xml
sh /opt/sonarqube-9.9.1.69595/bin/linux-x86-64/sonar.sh status
```

3. stop SonarQube using the following command:
``` xml
sh /opt/sonarqube-9.9.1.69595/bin/linux-x86-64/sonar.sh stop
```

### Step 10: Access SonarQube from Browser
Find the public IP of your EC2 instance from the EC2 dashboard.
``` xml
http://<your-ec2-public-ip>:9000
```

### Default SonarQube Credentials:
Username & Password 
```xml
admin
```
#### Note:
After logging in, it is strongly recommended to change the default password for security best practices.
