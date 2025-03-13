### . Introduction
Nagios is an open-source monitoring tool that provides real-time insights into the health of IT infrastructure
(servers, network devices, and applications). This project focuses on deploying Nagios Core to monitor local and remote systems,
ensuring proactive issue detection and resolution.

## Project Objective
- Install Nagios Core on a Linux server.
- Configure monitoring for local and remote hosts (CPU, disk, HTTP).
- Set up email notifications for critical alerts.
- Validate the monitoring system through testing

## Project Objective
- Prevent downtime caused by unresponsive services.
- Identify resource bottlenecks (e.g., disk space, CPU overload).=
- Lack of visibility into remote systems’ health.
- Nagios solves these challenges by offering a centralized, customizable monitoring solution with alerting capabilities.

## Methodology
- Requirements Analysis: Identify hardware/software prerequisites.
- Tool Selection: Choose Nagios Core for its flexibility and community support.
- Install dependencies (Apache, PHP, GCC).
- Compile and configure Nagios Core and plugins.
- Secure the web interface with Apache authentication.

- Define local and remote hosts/services.
- Configure email alerts for notifications.
- Integrate NRPE (Nagios Remote Plugin Executor) for remote monitoring.
- Validate configurations using nagios -v.
- Simulate failures to test alerts.
- Verify email notifications and dashboard metrics.

### Installation Process
  ``` sudo apt update && sudo apt upgrade -y
    sudo apt install -y apache2 php libapache2-mod-php build-essential libgd-dev openssl libssl-dev unzip
    wget https://assets.nagios.com/downloads/nagioscore/releases/nagios-4.4.6.tar.gz  
  tar -xzf nagios-4.4.6.tar.gz  
  cd nagios-4.4.6  
  ./configure --with-httpd-conf=/etc/apache2/sites-enabled  
  make all  
  sudo make install
```
### Configure Apache
```
sudo htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin
sudo a2enmod cgi rewrite  
sudo systemctl restart apache2
```
### Install Plugins
``` wget https://nagios-plugins.org/download/nagios-plugins-2.3.3.tar.gz  
tar -xzf nagios-plugins-2.3.3.tar.gz  
cd nagios-plugins-2.3.3  
./configure --with-nagios-user=nagios  
make  
sudo make install
```
### Configuration Details
``` /usr/local/nagios/etc/objects/localhost.cfg
define host {  
  use        linux-server  
  host_name  localhost  
  address    127.0.0.1  
}  

define service {  
  host_name           localhost  
  service_description CPU Load  
  check_command       check_nrpe!check_load  
}
```
### Results and Validation
``` sudo systemctl stop apache2  # Trigger HTTP service alert
```
### Conclusion
Nagios Core was successfully deployed to monitor local and remote systems. The system now provides real-time alerts, 
reducing downtime risks. Future enhancements could include monitoring additional services (e.g., databases) and integrating Grafana for visualization.
## nagios Dashboard
![nagio dashboard](https://github.com/rukevweubio/Nagios-Installation-and-Configuration-for-Network-Monitoring/blob/main/Screenshot%20(472).png)

![nagios dashboard](https://github.com/rukevweubio/Nagios-Installation-and-Configuration-for-Network-Monitoring/blob/main/Screenshot%20(471).png)

![nagios dashboard](https://github.com/rukevweubio/Nagios-Installation-and-Configuration-for-Network-Monitoring/blob/main/Screenshot%20(465).png)
## apache2 status 

![nagios dashboard](https://github.com/rukevweubio/Nagios-Installation-and-Configuration-for-Network-Monitoring/blob/main/Screenshot%20(477).png)
## nagios  status 

![nagios dashboard](https://github.com/rukevweubio/Nagios-Installation-and-Configuration-for-Network-Monitoring/blob/main/Screenshot%20(476).png)

