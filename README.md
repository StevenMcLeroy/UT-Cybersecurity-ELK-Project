# UT-Cybersecurity-ELK-Project

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Network_Diagram](https://user-images.githubusercontent.com/89950271/148111822-845aa347-69a6-44f9-a630-e22253fb161f.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  https://github.com/the-Coding-Boot-Camp-at-UT/UTA-VIRT-CYBER-PT-09-2021-U-LOL/blob/master/1-Lesson-Plans/13-Elk-Stack-Project/Activities/Stu_Day_1/Unsolved/Resources/install-elk.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build

### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the Damn Vulnerable Web Application.

Load balancing helps ensure that the application will be highly redundant and may be used to restrict unauthorized access to the network. In addition to providing redundancy (thus increasing availability) load balancers are advantageous given that they are hardened devices that both monitor traffic and control access to internal networks/resources. Furthermore, load balancers can protect against potential DDOS attacks and increase efficiency of network resources.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to system files and system resources.
  - Filebeat monitors alterations to log and system files.
  - Metricbeat logs and monitors system resources (CPU, memory, network statistics, etc.)

The configuration details of each machine may be found below.

|Name            |Function        |IP Address             |Operating System |
|----------------|----------------|-----------------------|-----------------|
|Ruby-Jump-Box   |Gateway         |10.2.0.4/23.99.207.162 |Linux (Ubuntu)   |
|Ruby-Web-1      |DVWA Web Server |10.2.0.5               |Linux (Ubuntu)   | 
|Ruby-Web-2      |DVWA Web Server |10.2.0.6               |Linux (Ubuntu)   |
|Ruby-Web-3      |DVWA Web Server |10.2.0.8               |Linux (Ubuntu)   |
|Ruby-ELK-Server |ELK Stack Server|10.3.0.4               |Linux (Ubuntu)   |  

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box Provisioner can accept connections from the Internet. Access to this machine is only allowed from the user’s public IP address. (User’s public IP address redacted given potential security ramifications.)

Machines within the network can only be accessed by SSH from the Jump Box Provisioner.
	Ruby-Jump-Box: 23.99.207.162 (Public IP)/10.2.0.4(Private IP)

A summary of the access policies in place can be found in the table below.

| Name           | Publicly Accessible | Allowed IP Addresses |
|----------------|---------------------|----------------------|
|Ruby-Jump-Box   |Yes                  |User’s IP Address     |
|Ruby-Web-1      |No                   |10.2.0.4              |
|Ruby-Web-2      |No                   |10.2.0.4              |
|Ruby-Web-2      |No                   |10.2.0.4              |
|Ruby-ELK-Server |No                   |User’s IP, 10.2.0.4   |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous given the efficiency and scalability of automation.

The playbook implements the following tasks:
	- Installs Docker.io
	- Installs Python-pip3
	- Downloads and configures the ELK container
	- Increase virtual memory of the ELK-Server
	- Activates ports 5601, 9200, and 5044
  
  The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![docker-ps](https://user-images.githubusercontent.com/89950271/148112550-ee40488d-8dd1-4a81-a8af-c3d80ccaf9ca.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
	
	Ruby-Web-1: 10.2.0.5
	Ruby-Web-2: 10.2.0.6
	Ruby-Web-3: 10.2.0.8

We have installed the following Beats on these machines:
	Filebeat
	Metricbeat

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to /etc/ansible/ directory
- Update the etc/ansible/hosts file to include the ELK sever
- Run the playbook, and navigate to http://<ELK.VM.External.IP>:5601/app/kibana to check that the installation worked as expected. As the ELK-Server uses a dynamic external IP address, be careful to use the appropriate IP for the session in question.

- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_


