## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(AzureNetworkDiagramm.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook and configurations files may be used to install only certain pieces of it, such as Filebeat.

- elk-playbook.yml
- filebeat-config.yml
- filebeat-playbook.yml
- metricbeat-config.yml
- metricbeat-playbook.yml
          

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
- Beats in Use
- Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting inbound traffic to the network.
Load balancers make the virtual network private and restrict inbound traffic unless permitted by the network sescurity group.
The Jump Box prevents subsequent virtual machines from being exposed to the public.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system performance.
Filebeat monitors log files and collects log event and forwards te information to Elasticsearch and/or Logstash. What does Metricbeat record? Metricbeat collects data (CPU usage, Memory usage, Disk usage) from operating systems and running services to monitor performance.

The configuration details of each machine may be found below.

| Name                 | Function          | IP Address    | Operating System |
|----------------------|-------------------|---------------|------------------|
| Jean Gray            | Jump Box/Ansible  | 10.0.0.4      | Linux            |
| Wolverine            | Docker            | 10.0.0.5      | Linux            |
| Beast                | Docker            | 10.0.0.6      | Linux            |
| LionO                | Elk Server        | 10.1.0.4      | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jean Gray machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 97.122.251.232 
- 10.0.0.4

Machines within the network can only be accessed by LionO (ELK Server 10.1.0.4).

A summary of the access policies in place can be found in the table below.

| Name            | Publicly Accessible | Allowed IP Addresses                        |
|-----------------|---------------------|---------------------------------------------|                       
| Jean Gray       | Yes                 | 97.122.251.232                              |
| Wolverine       | No                  | 52.247.197.19, 10.0.0.4, 10.0.0.6, 10.1.0.4 |
| Beast           | No                  | 52.247.197.19, 10.0.0.4, 10.0.0.5, 10.1.0.4 |
| LionO           | No                  | 52.247.197.19, 10.0.0.4, 10.0.0.5, 10.0.0.6 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because Ansible ensures that the provisioning scripts run identically each time and minimizes variability. 

The playbook implements the following tasks:
- The ELK installation play deploys a virtual machine allocated to the the ELK server.
- The ELK docker is then configured and downloads the docker images to the ansible VM and allows traffic to flow from web 1 & 2 to the ELK server VM
- The ELK server VM then captures the data (event logs, system log, VM/server performance metrics) in Kibana for further analysis 

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(Images/DockerPS.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5
- 10.0.0.6

We have installed the following Beats on these machines:
- Filebeat & Metricbeat

These Beats allow us to collect the following information from each machine:
Filebeat collects system log data and Metricbeat collects performance data such as CPU, Disk, and Memory usage. Winlogbeats reads from event logs using Windows API's, filters events based on user configured criteria, ans sends the event data to Elasticsearch of Logstash. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the elk-playbook file to /etc/ansible/.
- Update the elk-playbook file to include ports 5044, 5601 & 9200.
- Run the ansible-playbook elk-playbook.yml, and navigate to http://52.242.76.186:5601 to check that the installation worked as expected.
