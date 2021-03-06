## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Topology](https://github.com/wlaluz/Project-1/blob/main/Images/Project1-Topology.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

- [ansible.cfg.yml](https://github.com/wlaluz/Project-1/blob/main/Ansible/ansible.cfg)
- [fileBeats.config.yml](https://github.com/wlaluz/Project-1/blob/main/Ansible/filebeat-config.yml)
- [FileBeats-Playbook.yml](https://github.com/wlaluz/Project-1/blob/main/Ansible/filebeat-config.yml)
- [metric.config.yml](https://github.com/wlaluz/Project-1/blob/main/Ansible/metricbeat-config.yml)
- [metric-playbook.yml](https://github.com/wlaluz/Project-1/blob/main/Ansible/metricbeat-playbook.yml)
- [pentest.yml](https://github.com/wlaluz/Project-1/blob/main/Ansible/Pentest.yml)
- [install-elk.yml](https://github.com/wlaluz/Project-1/blob/main/Ansible/install-elk.yml)


This document contains the following details:
- Description of the Toplogy
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly avaliable, in addition to restricting access to the network.
The Load balancers protect against DDOS attacks. One of the advantages of a jump box is that it's a secure way of accesseing your private environment. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
- Filebeats watches for file System Logs. 
- Metricbeat records the performance of the machines you are monitoring. It looks at CPU, Memory and Disk Usage. 

The configuration details of each machine may be found below.


| Name     | Function  | IP Address | Operating System |
|----------|-----------|------------|------------------|
| Jump Box | Gateway   | 10.0.0.1   | Linux            |
| Elk-VM   | Monitor   | 10.1.0.4   | Linux            |
| Web-1    | Webserver | 10.0.0.5   | Linux            |
| Web-2    | Webserver | 10.0.0.6   | Linux            |
| DVWA-VM3 | Webserver | 10.0.0.7   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP address:
- My home network

Machines within the network can only be accessed by The Jump Box.
The Jump Box IP is: 10.0.0.7. 

A summary of the access policies in place can be found in the table below.

| Name               | Publicly Accessible | Allowed IP Addresses |
|--------------------|---------------------|----------------------|
| Jump Box : 22      | Yes                 | Home Network         |
| Load Balancer : 80 | Yes                 | Home Network         |
| Elk-VM: 5601       | Yes                 | Home Network         |
| Elk-VM: 22         | No                  | 10.0.0.7             |
| Webserver : 22     | No                  | 10.0.0.7             |
### Elk Configuration


Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because a server can crash and you will be able to bring up a new server in minutes with Ansible automating configuration. 

The playbook implements the following tasks:
- Install Docker.io
- Install pip3
- Install Docker python module
- Use More memory
- Download and launch a docker elk container
- Enable service docker on boot  

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![docker ps](https://github.com/wlaluz/Project-1/blob/main/Images/Docker%20PS.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1: 10.0.0.5
- Web-2: 10.0.0.6
- DVWA-VM3: 10.0.0.4

We have installed the following Beats on these machines:
- Filebeats
- Metricbeats 

These Beats allow us to collect the following information from each machine:
-Filebeat: Filebeats collects logs about the file system, such as those generated by Apache, Microsoft Azure tools. 
-Metricbeat: This is like a task manager for a vitual envirnoment. It collects CPU utlization, Memory usage, and other system metrics. 

![MetricBeat-Example](https://github.com/wlaluz/Project-1/blob/main/Images/MetricBeat.png)

![FileBeat-Example](https://github.com/wlaluz/Project-1/blob/main/Images/FileBeat.png)

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to /etc/ansible.
- Update the host file to include the new Elk group and add the target Elk IP. 
- Run the playbook, and navigate to Kibana on your browser via http://{Elk Pubic IP}:5601/app/kibana to check that the installation worked as expected.

