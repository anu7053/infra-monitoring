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

