# infra-monitoring
This is to setup infra monitoring tools, such as Grafana, Prometheus and Opentelemetry etc.
------------------------------------------------------------------------------------------

This command adds the official Grafana stable repository to your package manager
###
cat <<EOF | sudo tee /etc/yum.repos.d/grafana.repo
[grafana]
name=grafana
baseurl=https://rpm.grafana.com
repo_gpgcheck=1
enabled=1
gpgcheck=1
gpgkey=https://rpm.grafana.com/gpg.key
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt
EOF

## To install Grafana Enterprise (Recommended by Grafana):
sudo yum install -y grafana-enterprise
## To install Grafana Open Source (OSS)
sudo yum install -y grafana

## ### NOT starting on installation, please execute the following statements to configure grafana to start automatically using systemd
 sudo /bin/systemctl daemon-reload
 sudo /bin/systemctl enable grafana-server.service
### You can start grafana-server by executing
 sudo /bin/systemctl start grafana-server.service
## : Start and Enable the Service

# Reload the systemd manager configuration
sudo systemctl daemon-reload

# Start the Grafana server
sudo systemctl start grafana-server

# Enable Grafana to start automatically on boot
sudo systemctl enable grafana-server

## sudo systemctl enable grafana-server
sudo systemctl status grafana-server
## Check Service Status
sudo systemctl status grafana-server

## Local Connectivity Check
curl http://localhost:3000/api/health

## check the local access via your ec2 pub id with http://<ec2-ip>:3000



## As a Grafana developer you may not need to know 
these things as these are generally required by 
Administrator who manages your environment. 
However It is good to know these details, So I am 
compiling them here. 
 
## Important Details About Grafana 
Item Detail Description 
## Default Port 3000 This is the default port of Grafana on which Grafana 
services listens on. This port can be changed (if 
required) by making changes in Grafana 
configuration file and Restarting Grafana. 
## Log File /var/log/grafana/grafana.log This is where Grafana writes all the logs. If you have 
issue in Grafana then you can check this log files to 
know about the error message and troubleshoot. 
## Configuration File Path /etc/grafana/grafana.ini This is Grafana configuration File. This contains all 
configuration information about Grafana.  
 
## his is the file you would be making changes in if you 
want to change things like SMTP configuration, 
Database Change, Port Change etc.  
## Managing Services • sudo systemctl 
status grafana 
## • sudo systemctl  stop 
grafana 
## • sudo systemctl  start 
grafana 
## • sudo systemctl  
restart grafana 

Use these commands to Check Status of Grafana 
Service, Stop, Start or Restart Grafana Service. 
## Uninstall Grafana sudo yum remove -y grafana This will uninstall Grafana. 
   
## Important Details About InfluxDB 
Item Detail Description 
## Default Port 8086 By Default InfluxDB runs on 
# port 8086 which can be 
changed by making changes in 
influxDB configuration file and 
restarting InfluxDB. 
# Log File sudo journalctl -u 
influxdb.service To check logs of InfluxDB on 
Linux, use this command. 
## Configuration File /etc/influxdb/influxdb.conf This is the default location of 
InfluxDB configuration file. If 
you want to make changes 
such as InfluxDB default port, 
than this is the place where 
you should be looking at. 
## Managing Services • sudo systemctl status 
influxdb 
## • sudo systemctl  stop 
influxdb 
## • sudo systemctl  start 
influxdb 
## • sudo systemctl  restart 
influxdb 
 
Use these commands to Check 
Status of InfluxDB Service, 
Stop, Start or Restart InfluxDB 
Service. 
## Uninstall InfluxDB • sudo yum remove -y 
influxdb 
This will uninstall InfluxDB 
   
Important Details About Telegraf 
Item 
Detail 
Log File 
## sudo journalctl -u 
Description 
# telegraf.service 
Configuration File 
To check logs of Telegraf on 
# Linux, use this command. 
## /etc/telegraf/telegraf.conf This is the default location of 
Telegraf configuration file. If 
you want to make changes 
such as Telegraf inputs or 
outputs. 
Managing Services 
# • sudo systemctl status 
telegraf 
# • sudo systemctl  stop 
telegraf 
Use these commands to Check 
Status of Telegraf Service, 
Stop, Start or Restart Telegraf 
Service. 
# • sudo systemctl  start 
telegraf 
#• sudo systemctl  restart 
telegraf 
Uninstall InfluxDB 
# • sudo yum remove -y 
telegraf

## How to reset Grafana password

# sudo grafana-cli --homepath "/usr/share/grafana" --config "/etc/grafana/grafana.ini" admin reset-admin-password Meest@123456
## run below command if unable to reset admin username & password

# sudo grafana-cli --homepath "/usr/share/grafana" --config "/etc/grafana/grafana.ini" admin reset-admin-password --password-from-stdin




