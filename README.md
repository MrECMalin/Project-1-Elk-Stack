## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![alt text](https://github.com/MrECMalin/Project-1-Elk-Stack/blob/main/Unit%2012%20Azure%20Diagram.jpg)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

[ELK Playbook](https://github.com/MrECMalin/Project-1-Elk-Stack/blob/main/ELK_playbook.yml)

[Filebeat Playbook](https://github.com/MrECMalin/Project-1-Elk-Stack/blob/main/filebeat-playbook.yml)

[Metricbeat Playbook](https://github.com/MrECMalin/Project-1-Elk-Stack/blob/main/metricbeat_playbook.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

Load balnacers protects against DDoS attacks by shifting the traffic load. A jump box has the advantage of being a single point where users can be managed and traffic can be monitored.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash. 

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| ELK Server  | Monitor  | 10.1.0.4   | Linux            |
| Web-1    | Servers  | 10.0.0.5   | Linux            |
| Web-2    | Servers  | 10.0.0.6   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump box provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
10.225.13.126

Machines within the network can only be accessed by the jump box.
The Elk machine can have access from 10.225.13.126 through port 22

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                  | 10.225.13.126    |
| Load Balancer  |   Yes        |   Open                   |
|  Web 1        |  No                   |  10.0.0.5                   |
|  Web 2        |  No                   |  10.0.0.6                   |
|  ELK Server        |  Yes                   |  10.225.13.126   |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because system installation and updating can be simplified, the number of services can be restricted, and processes can be replicated.

The playbook implements the following tasks:

- Install docker.io
 
- Install pip3
 
- Install Docker python module
 
- Increase virtual memory
 
- Download and launch a docker

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![alt text](https://github.com/MrECMalin/Project-1-Elk-Stack/blob/main/dockerps.jpg)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

10.0.0.5 
10.0.0.6

We have installed the following Beats on these machines:

FileBeat 
MetricBeat

These Beats allow us to collect the following information from each machine:

Filebeat forwards and centralizes log data. It can handle audit logs, deprecation logs, gc logs, server logs, and slow logs.

MetricBeat collects metrics from the operating system such as CPU or memory and from services running on the server. It can also be used to monitor other beats and ELK stack itself.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

- Copy the configuration file to your web VMs.
- Update the /etc/ansible/hosts file to include the IP addresses of the ELK server, VM, and webservers.
- Run the playbook, and navigate to http://10.225.13.126:5601/app/kibana to check that the installation worked as expected.

The playbook file is filebeat-configuration.yml which you would copy from /etc/ansible/files/filebeat-configuration.yml to /etc/filebeat/filebeat-configuration.yml

To make Ansible run the playbook on a specific machine you update filebeat-configuration.yml.  To specify which machine to install the ELK server on versus which to install Filebeat on you would navigate to the host files and update them with the IP addresses of web servers as well as the Elk server and select which group to run in Ansible.

In order to check that the ELK server is running navigate to http://10.225.13.126:5601/app/kibana
