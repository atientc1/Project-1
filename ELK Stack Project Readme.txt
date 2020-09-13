These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

elkstack_project_diagram.gliffy

This document contains the following details:

Description of the Topology
Access Policies
ELK Configuration
-Beats in Use
-Machines Being Monitored
How to Use the Ansible Build


Description of the Topology
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
Load balancing ensures that the application will be highly available, in addition to restricting only secured access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system metrics.

The configuration details of each machine may be found below.
Note: Use the Markdown Table Generator to add/remove values from the table.


|Name|Function|IP Address|Operating System|
|----|--------|----------|----------------|
|Jump-Box-Provisioner|Gateway|10.0.0.4,51.143.14.221|Linux|
|Web1|DVWA|10.0.0.5|Linux|
|Web2|DVWA|10.0.0.6|Linux|   
|ELKSTACK-Server|ELKStack Container|10.1.0.4,104.44.133.19|Linux|

Access Policies
The machines on the internal network are not exposed to the public Internet.
Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

HOME IP

Machines within the network can only be accessed by Jump-Box-Provisioner (10.0.0.4,51.143.14.221).

A summary of the access policies in place can be found in the table below.

| Name  | Publicly Accessible|Allowed IP Addresses|
|-------|--------------------|--------------------|
|Jump-Box-Provisioner|Yes|HOME IP|
|Web1|No|10.0.0.4,51.143.14.221|
|Web2|No|10.0.0.4,51.143.14.221| 
|ELKSTACK-Server|Yes|10.0.0.4,51.143.14.221|

Elk Configuration
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it made it easier to update groups of server with the same exact processes.

The playbook implements the following tasks:
-Repo key download
-Make sure Docker repo is installed
-Uninstall Apache2
-Install docker-ce
-Install docker-ce-cli
-Install containerd.io
-Install python3-pip
-Install Python Docker Module
-Download and launch DVWA

The following screenshot displays the result of running docker ps after successfully configuring the ELK instance.
DockerPS_ElkStack_Server_Pic.PNG

Target Machines & Beats
This ELK server is configured to monitor the following machines:
-Web1 (10.0.0.5)
-Web2 (10.0.0.6)

We have installed the following Beats on these machines:
-Filebeat
-Metricbeat

These Beats allow us to collect the following information from each machine:
-Filebeat is designed to read files from your system. It is particularly useful for system and application log files, but can be used for any text files that you would like to index to Elasticsearch in some way. In the logging case, it helps centralize logs and files in an efficient manner by reading from your various servers and VMs, then shipping to a central Logstash or Elasticsearch instance. Additionally, Filebeat eases the configuration process by including “modules” for grabbing common log file formats from MySQL, Apache, NGINX and more. These modules reduce the Filebeat configuration to a single command.
-Metricbeat is used to collect metrics from servers and systems. It is a lightweight platform dedicated to sending system and service statistics. Like Filebeat, Metricbeat includes modules to grab metrics from operating systems like Linux, Windows and Mac OS, applications such as Apache, MongoDB, MySQL and nginx. Metricbeat is extremely lightweight and can be installed on your systems without impacting system or application performance. As with all of the Beats, Metricbeat makes it easy to create your own custom modules.

Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:
SSH into the control node and follow the steps below:

Copy the ansible.cfg file to etc/ansible
Update the hosts configuration file to include correct private IP address of ELKSTACK-Server
Run the playbook, and navigate to Kibana (ELKSTACK-ServerIP:5601) to check that the installation worked as expected.

