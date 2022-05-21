# ELK-Stack-Project
We've been given a project to create and discuss an ELK Stack via Windows Azure.
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

!/Users/angeldanois/ELK-Stack-Project/Diagrams/Diagram.drawio.pdf

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  - /Users/angeldanois/ELK-Stack-Project/Ansible/Install-elk.yml.txt
  - /Users/angeldanois/ELK-Stack-Project/Ansible/install-docker.yml.txt
  - /Users/angeldanois/ELK-Stack-Project/Ansible/install-metricbeat.yml.txt
  - /Users/angeldanois/ELK-Stack-Project/Ansible/filebeat-playbook.yml.txt

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

- Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
- Load balancers prioritize and protect the availability of a service and ward off potential DDos attacks. Jump boxes allow for a single secured point of entry that can be monitored as opposed to several different machines needing to be kept track of on a public network. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system metrics.
- Filebeats watches for specific log files and collects log events.
- Metricbeat records metrics and statistics from a system and from any services running on that server.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  |  10.0.0.1  | Linux            |
| Web-1    | VM       |  10.0.0.5  | Linux            |
| Web-2    | VM       |  10.0.0.6  | Linux            |
| Elk-VM   | ELK Stack|  10.1.0.4  | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
 24.30.16.129

Machines within the network can only be accessed by Port 22.
My own IP address 24.30.16.129 was able to access the ELK VM via ssh.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box |   Yes               | 24.30.16.129         |
|  Web-1   |   No                |   10.0.0.4           |
|  Web-2   |   No                |   10.0.0.4           |
| ELK Stack|   No                | 20.248.171.133       |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

It allows for easy deployment on multiple machines at once which removes the possibility of human error.

The playbook implements the following tasks:
- Install docker
- Install pip3
- Install docker python module
- Download and launch a docker web container
- Enable docker

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

/Users/angeldanois/Downloads/README/Images/sudo-docker-ps.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
10.1.0.4
10.0.0.5
10.0.0.6

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeats collects logs and watches for specific log files, much like an activity monitor on a system. Metricbeat collects metrics and statistics on a system, this is similar to storage monitoring on a device in order to ensure proper performance and space.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml file to /etc/ansible/files.
- Update the config file to include the IP addresses of the virtual machines.
- Run the playbook, and navigate to Kibana to check that the installation worked as expected.

- _Which file is the playbook? Where do you copy it?_

Install-elk.yml and it is copied to the /etc/ansible directory.

- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_

Update filebeat-config.yml and specify which machine to install the ELK server via the host files and inputting the IP addresses of the web and elk machines. To specify which machine to install the ELK server versus Filebeat you can specify the group in the same host file.

- _Which URL do you navigate to in order to check that the ELK server is running?

http://[elkserverpublicIP]:5601/app/kibana
