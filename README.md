## Gilbert Gualberto Jr
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - [YML file Playbook Guide for filebeat installation](../Files/filebeat-playbook.yml)

### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly _____, in addition to restricting _____ to the network.
- What aspect of security do load balancers protect?
	- Protect applications from emerging threats
		- The Web Application Firewall (WAF) in the load balancer protects your website from hackers and includes daily rule updates just like a virus scanner

	- Authenticate User Access
		- The load balancer can request a username and password before granting access to your website to protect against unauthorized access

	- Protect against DDoS attack
		- The load balancer can detect and drop distributed denial-of-service (DDoS) traffic before it gets to your website

	- Simplify PCI compliance
		- If you process credit cards, you need to comply with Payment Card Industry (PCI) regulations. A load balancer simplifies compliance with PCI rules

What is the advantage of a jump box?
- Improve productivity: Jump servers make it possible for the admin to do his or her work on the two sub-networks without the time-wasting process of logging out and logging back into each privileged area. It provides effective access control. In a multi-tenant environment like a co-location facility, an administrator may need to perform tasks like running Microsoft Remote Desktop Protocol (RDP) sessions on multiple client systems. Without a jump server, or a comparable privileged access device, the work will slow down significantly.
	- Improve security: Jump servers create separation between a user’s workstation (which is at high risk of being compromised) and the privileged assets within the network. This separation helps to isolate privileged assets so that they are not directly in contact with potentially compromised workstations. In addition, because of their access to potentially sensitive areas, jump servers are usually “hardened” in the extreme, i.e. it’s not easy to install software on them, update their firmware and so forth. They’re never used for non-administrative work and access is tightly controlled and monitored. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _____ and system _____.
- What does Filebeat watch for?
	- Filebeat is a lightweight shipper for forwarding and centralizing log data. Installed as an agent on your servers, Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing
- What does Metricbeat record?
	- Metricbeat is a lightweight shipper that you can install on your servers to periodically collect metrics from the operating system and from services running on the server. Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.
		- Metricbeat helps you monitor your servers by collecting metrics from the system and services running on the server, such as:

			- Apache
			- HAProxy
			- MongoDB
			- MySQL
			- Nginx
			- PostgreSQL
			- Redis
			- System
			- Zookeeper

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name       | Function | IP Address | Operating System |
|------------|----------|------------|------------------|
| Jump Box   | Gateway  | 10.0.0.4   | Linux            |
| Web-1      | Gateway  | 10.0.0.5   | Linux            |
| Web-2      | Gateway  | 10.0.0.6   | Linux            |
| ELK-Server | Gateway  | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JBOX machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Add whitelisted IP addresses
	- All IP addresses that are not inside the network

Machines within the network can only be accessed by JBOX.
- Which machine did you allow to access your ELK VM? What was its IP address?
	- JBOX IP address 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 10.0.0.5 10.0.0.5    |
| Web-1    | No                  | 10.0.0.4             |
| Web-2    | No                  | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible?
	- Agentless. There are no agents or software deployed on the clients/servers to work with Ansible. The connection can be done through the SSH or using the Python.
	- To use the Ansible, configure, and deploy the infrastructure is very simple and it is English like the language used called YAML.
	- The Ansible Playbook can be used to write programs or the modules and can be used to manage the IT without any downside

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- Install: docker.io
- Install: python-pip
- Install: docker
- Command: sysctl -w vm.max_map_count=262144
- Launch docker container: ELK-Server 

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Update the path with the name of your screenshot of docker ps output](Images/elkserver.jpg)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- List the IP addresses of the machines you are monitoring
	- Web-1 10.0.0.4
	- Web-2 10.0.0.5

We have installed the following Beats on these machines:
- Specify which Beats you successfully installed_
	- Filebeat
	- Metricbeat

These Beats allow us to collect the following information from each machine:
- In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc.
	- Metricbeats takes the metric and statistics that collects and ships the specified output. And the Filebeat monitors the log files or locations that specify, collects log events, and forward it for indexing.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

Answer the following questions to fill in the blanks:
- Which file is the playbook? Where do you copy it?
	-/etc/ansible/file/filebeat-configuration.yml
- Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
	- /etc/ansible/host should be edit and should be added to Web-1, Web-2 and ELK-Server IP address
- Which URL do you navigate to in order to check that the ELK server is running?
	- http://13.68.248.95:5601/app/kibana#/home (Public ip + port #)
As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc.
	- anisble-playbook
	- filebeat-playbook.yml
