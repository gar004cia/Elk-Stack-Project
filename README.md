## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Cloud-Network-Diagram.png](Images/Cloud_Network_Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Config/Playbook file may be used to install only certain pieces of it, such as Filebeat.


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly accessible, in addition to restricting traffic to the network.
- What is the advantage of a jump box?_ Load balancers protect layer 4, which is the transport of data. Having a jump box allows for an additional layer of security. The jump box is the only machine that can access the virtual network. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the performance and system logs.
- Filebeat monitors and collects log files from our VMs. Filebeat sends these log files to Logstash and Elasticsearch. 
- Metricbeat monitors the health of a computer. Metricbeat looks at metrics such as CPU usage and the computer's uptime.

The configuration details of each machine may be found below.

| Name       | Function   | IP Address | Operating System |
|------------|------------|------------|------------------|
| Jump Box   | Gateway    | 10.0.0.7   | Linux            |
| Web-1      | Webserver  | 10.0.0.5   | Linux            |
| Web-2      | Webserver  | 10.0.0.4   | Linux            |
| Web-3      | Webserver  | 10.0.0.6   | Linux            |
| Elk-Server | Monitoring | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: 70.120.51.231 which is "my workstation"

Machines within the network can only be accessed by the Jump Box, with an IP of 10.0.0.7.

A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible | Allowed IP Addresses     |
|------------|---------------------|--------------------------|
| Jump Box   | Gateway             | 70.120.51.231            |
| Web-1      | Webserver           | 10.0.0.7                 |
| Web-2      | Webserver           | 10.0.0.7                 |
| Web-3      | Webserver           | 10.0.0.7                 |
| Elk-Server | Monitoring          | 70.120.51.231 & 10.0.0.7 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it minimizes errors and keeps us from having to install software directly to the host machine. Rather the ansible container was used to distribute the software. Ansible allowed also simplified this process by installing and configuring the VM all at once. 


The playbook implements the following tasks:
- Install docker.io
- Install pip3
- Install Docker python module
- Update to use more memory (262144) 
- Download and launch a docker elk container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![docker-ps-output.png](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 10.0.0.5
- Web-2 10.0.0.4
- Web-3 10.0.0.6

We have installed the following Beats on these machines:
- Filebeat & Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat will be monitoring system logs of each of the VMs. For example filebeat will be monitoring sudo commands, SSH logins and new users/groups on our virtual machines. 
- Metricbeat is monitoring the "health" of our virtual machines. One key metric that is looked at is CPU usage. If CPU usage is high that could potentially mean the machine is being used for nefarious activity.


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk file to the install-elk.yml file.
- Update the hosts file to include the Elk-Server's IP address. This will insure that when running the  install-elk.yml file, it downloads and runs the elk server container on that VM (Elk-Server). 
- Run the playbook, and navigate to http://[Elk-Server public IP]:5601/app/kibana to check that the installation worked as expected.
