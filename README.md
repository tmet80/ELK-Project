## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(AzureNetworkDiagramm.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  -_TODO: ansible.cfg,
           docker.yml,
           elk-playbook.yml,
           filebeat-config.yml,
           filebeat-playbook.yml,
           hosts,
           metricbeat-config.yml,
           metricbeat-playbook.yml,
           pentest.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting inbound traffic to the network.
- _TODO:  What aspect of security do load balancers protect? Load balancers make the virtual network private and restrict inbound traffic unless permitted by the network       sescurity group.
         What is the advantage of a jump box? The Jump Box prevents subsequent virtual machines from being exposed to the public.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _____ and system _____.
- _TODO: What does Filebeat watch for? Filebeat monitors log files and collects log event and forwards te information to Elasticsearch and/or Logstash.
- _TODO: What does Metricbeat record? Metricbeat collects data (CPU usage, Memory usage, Disk usage) from operating systems and running services to monitor performance.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name                 | Function          | IP Address    | Operating System |
|----------------------|-------------------|------------   |------------------|
| Jean Gray            | Jump Box/Ansible  | 10.0.0.4      | Linux            |
| Wolverine            | Docker            | 10.0.0.5      | Linux            |
| Beast                | Docker            | 10.0.0.6      | Linux            |
| LionO                | Elk Server        | 10.1.0.4      | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the ____machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _TODO: 97.122.251.232, 10.0.0.4

Machines within the network can only be accessed by _____.
- _TODO: Which machine did you allow to access your ELK VM? LionO What was its IP address? 10.1.0.4

A summary of the access policies in place can be found in the table below.

| Name           | Publicly Accessible | Allowed IP Addresses                        |
|----------      |---------------------|----------------------                       |
|Jean Gray       | Yes                 | 97.122.251.232                              |
|Wolverine       | No                  | 52.247.197.19, 10.0.0.4, 10.0.0.6, 10.1.0.4 |
|Beast           | No                  | 52.247.197.19, 10.0.0.4, 10.0.0.5, 10.1.0.4 |
|LionO           | No                  | 52.247.197.19, 10.0.0.4, 10.0.0.5, 10.0.0.6 |
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible? Ansible ensures that the provisioning scripts run identically each time and minimizes variability. 

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- The ELK installation play deploys a virtual machine allocated to the the ELK server.
- The ELK docker is then configured and downloads the docker images to the ansible VM and allows traffic to flow from web 1 & 2 to the ELK server VM
- The ELK server VM then captures the data (event logs, system log, VM/server performance metrics) in Kibana for further analysis 

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO:(Images/DockerPS.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: 10.0.0.5, 10.0.0.6

We have installed the following Beats on these machines:
- _TODO: Filebeat & Metricbeat

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
Filebeat collects system log data and Metricbeat collects performance data such as CPU, Disk, and Memory usage. Winlogbeats reads from event logs using Windows API's, filters events based on user configured criteria, ans sends the event data to Elasticsearch of Logstash. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it? The playbook file that has been copied is filebeat-config.yml; filebeat=config is copied into /etc/filebeat/filebeat.yml
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on? The hosts file is updated to ensure that the playbook runs on specific machines. To specify the maching to install ELK server ensure that the host line in the playbook is set to elk. For Filebeat, ensure that the host is set to webservers to install the playbook on the webserver machines.
- _Which URL do you navigate to in order to check that the ELK server is running? http://52.242.76.186.5601

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
