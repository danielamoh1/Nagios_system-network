# Nagios_system-network

### Project Overview:
1. **Nagios for System and Network Monitoring:**
   - Implement Nagios Core on a Linux server.
   - Configure Nagios to monitor critical system metrics (CPU, Memory, Disk) and network services (SSH, HTTP).
   - Create custom Nagios plugins for specialized monitoring needs using Bash or Python scripts.

2. **Suricata for Intrusion Detection:**
   - Install and configure Suricata on a network gateway or a dedicated monitoring interface.
   - Set up Suricata to analyze network traffic for signs of intrusion using community-sourced or custom rules.
   - Integrate Suricata alerts with Nagios for comprehensive monitoring and alerting.

3. **Automation with Ansible:**
   - Use Ansible to automate the deployment and configuration of Nagios and Suricata across multiple Linux servers.
   - Develop Ansible playbooks for consistent and repeatable setup.

4. **Web Dashboard:**
   - Implement a web-based dashboard using Grafana or a similar tool to visualize Nagios and Suricata data.
   - Customize the dashboard for real-time monitoring and historical analysis.

### Steps to Proceed:
1. **Environment Setup:** Prepare your Linux servers (preferably CentOS or Ubuntu) for Nagios and Suricata.
2. **Nagios Installation & Configuration:** Follow the official Nagios Core documentation for installation and set up basic monitoring.
3. **Suricata Installation & Configuration:** Install Suricata from official sources and configure it for network traffic analysis.
4. **Integration & Automation:** Develop scripts for integration and use Ansible for automation.
5. **Dashboard Development:** Set up Grafana and integrate it with Nagios and Suricata for a comprehensive monitoring view.
6. **Testing & Documentation:** Test the entire setup thoroughly and document the setup process, configuration, and usage in a README file for GitHub.

###########################################################################################################


Environment Setup for Nagios
Nagios Core Installation on CentOS:

```bash
sudo yum install -y gcc glibc glibc-common wget unzip httpd php gd gd-devel perl postfix
cd /tmp
wget https://assets.nagios.com/downloads/nagioscore/releases/nagios-4.4.6.tar.gz
tar xzf nagios-*.tar.gz
cd nagios-*
./configure --with-httpd-conf=/etc/httpd/conf.d
make all
sudo make install
sudo make install-commandmode
sudo make install-init
sudo make install-config
sudo make install-webconf
sudo htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin
sudo systemctl restart httpd.service
```

***Configure Nagios to Monitor System Metrics and Network Services:***

Add hosts and services to be monitored in /usr/local/nagios/etc/nagios.cfg.
Create custom plugins in /usr/local/nagios/libexec/ using Bash or Python for specialized monitoring needs.
Suricata for Intrusion Detection
Suricata Installation on Ubuntu
Install Suricata:

```bash
sudo add-apt-repository ppa:oisf/suricata-stable
sudo apt-get update
sudo apt-get install suricata
```
***Configure Suricata for Network Traffic Analysis:***

Edit /etc/suricata/suricata.yaml to set up network interfaces and specify rule files.
Use community-sourced rules or create custom rules in /etc/suricata/rules/.
Automation with Ansible
Ansible Playbooks for Nagios and Suricata Deployment:
Create an Ansible playbook deploy_nagios.yml to automate Nagios installation and configuration.
Develop deploy_suricata.yml for Suricata setup across Linux servers.
Web Dashboard with Grafana
Grafana Installation and Configuration:

```bash
sudo apt-get install -y software-properties-common
sudo add-apt-repository "deb https://packages.grafana.com/oss/deb stable main"
wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -
sudo apt-get update
sudo apt-get install grafana
sudo systemctl start grafana-server
sudo systemctl enable grafana-server
```

***Integrate Grafana with Nagios and Suricata:***

Set up data sources in Grafana for Nagios and Suricata metrics and logs.
Customize Grafana dashboards for monitoring and analysis.

***Testing & Documentation***

Thoroughly Test the Setup:
Ensure Nagios correctly monitors specified metrics and services.
Verify Suricata detects intrusions as per the configured rules.


==========================================================================================================================================

More in depth practical steps guides

1. **Set Up Network Interfaces:**
Open /etc/suricata/suricata.yaml and find the section af-packet:. Here, specify the network interface you want Suricata to monitor.

2. **Specify Rule Files:**
In the same suricata.yaml file, locate the rule-files: section and include your desired rule files. You can use community-sourced rules like Emerging Threats or your custom rules.

3. **Custom Rules:**
If creating custom rules, add them to /etc/suricata/rules/ directory. Example of a custom rule file custom.rules:
```
alert tcp any any -> any 80 (msg:"Possible HTTP traffic detected"; sid:1000001;)
```
