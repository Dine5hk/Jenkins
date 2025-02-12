# Jenkins

## Create an Instance 
![image](https://github.com/user-attachments/assets/00c40c51-c616-40cb-a755-298162c74572)
instance 
> Nginix and Jenkins in one instance
> Grafana and promotheous for monitoring
> SonarQube for code quality check

# Security group 
![image](https://github.com/user-attachments/assets/1c8135d7-d237-4263-9ec1-4dcc941c5391)

# Download the required packages 
> Nginix and Jenkins in one instance

```
sudo apt update
sudo apt install fontconfig openjdk-17-jre
```
# to install jenkins
```
 sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
            https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
            echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
            https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
            /etc/apt/sources.list.d/jenkins.list > /dev/null
            sudo apt-get update
            sudo apt-get install -y jenkins
```
# To start Jenkins Server 
```
sudo systemctl enable jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins
```
# To install nginix
```
sudo apt update -y
sudo apt install nginix
sudo apt update
```
# To start njinix server
```
sudo systemctl enable nginix
sudo systemctl start nginix
sudo systemctl status nginix
```

# Install node exporter for to get metrics value from the server

```
wget https://github.com/prometheus/node_exporter/releases/download/v1.8.2/node_exporter-1.8.2.linux-amd64.tar.gz
tar -xvf node_exporter-1.8.2.linux-amd64.tar.gz -C /home/ubuntu/prometheus
```


# For Promotheous and grafana Instance

```
sudo apt-get update
    mkdir /home/ubuntu/grafana
    sudo apt-get install -y adduser libfontconfig1 musl
    wget https://dl.grafana.com/enterprise/release/grafana-enterprise_8.2.3_amd64.deb
    sudo dpkg -i grafana-enterprise_8.2.3_amd64.deb
```
# to start grafana server
```
    sudo systemctl enable grafana-server
    sudo systemctl start grafana-server
```
# To install promotheous
```
wget https://github.com/prometheus/prometheus/releases/download/v3.0.1/prometheus-3.0.1.linux-amd64.tar.gz
wget https://github.com/prometheus/alertmanager/releases/download/v0.28.0-rc.0/alertmanager-0.28.0-rc.0.linux-amd64.tar.gz
wget https://github.com/prometheus/node_exporter/releases/download/v1.8.2/node_exporter-1.8.2.linux-amd64.tar.gz
```
# To untar folders
```
    mkdir /home/ubuntu/prometheus
    tar -xvf prometheus-3.0.1.linux-amd64.tar.gz -C /home/ubuntu/prometheus
    tar -xvf alertmanager-0.28.0-rc.0.linux-amd64.tar.gz -C /home/ubuntu/prometheus
    tar -xvf node_exporter-1.8.2.linux-amd64.tar.gz -C /home/ubuntu/prometheus
```
# To start promotheous server
```
sudo systemctl enable prometheus
sudo systemctl start prometheus
```
# To install SonarQube
```
sudo apt update
sudo apt upgrade
```
```
wget https://binaries.sonarsource.com/CommercialDistribution/sonarqube/sonarqube-9.5.0.56709.zip
unzip sonarqube-9.5.0.56709.zip
sudo mv sonarqube-9.5.0.56709 /opt/sonarqube
sudo useradd sonar -d /opt/sonarqube -M -r -s /bin/false
sudo chown -R sonar:sonar /opt/sonarqube
sudo nano /etc/systemd/system/sonar.service
```

# To setup SonarQube in sonar.service

```
[Unit]
Description=SonarQube service
After=network.target

[Service]
Type=forking
ExecStart=/opt/sonarqube/bin/linux-x86-64/sonar.sh start
ExecStop=/opt/sonarqube/bin/linux-x86-64/sonar.sh stop
User=sonar
Group=sonar
LimitNOFILE=65536
LimitNPROC=4096
LimitCORE=infinity

[Install]
WantedBy=multi-user.target
```
# start sonarqube

```
sudo systemctl daemon-reload
sudo systemctl start sonar
sudo systemctl enable sonar
sudo ufw allow 9000/tcp
```

# Step 2 setup in GitHub Token

> Go to github settings--> Developer Settings
![image](https://github.com/user-attachments/assets/3d0d0b67-9b1c-4a20-b085-432c8c61ad99)

> Developer Setting--> Click Classic Tokens and Generate new token
# enable the nessesary scopes
![image](https://github.com/user-attachments/assets/ae39945b-4920-4ee8-b329-a9c0ed0c5795)

# Go to jenkins page (eg: ip-address:8080)
> to find the initial password in jenkins ec2 server for login 
```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```
> Goto managa jenkins and in plugins install the nessessary package
```
sonarqube
github
```
> Go to new Items and create new freestyle project
![image](https://github.com/user-attachments/assets/275b5002-a8b4-43c3-bed7-e9d3a3646957)

# In ssh jenkins server to create, add and give permission to jenkins

```
