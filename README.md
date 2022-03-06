## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram]https://github.com/PCharleigh/ElkProject/blob/main/Diagrams/Virtual%20Network%20Diagram%20-%20Page%203.pdf

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook.yml file may be used to install only certain pieces of it, such as Filebeat.

  -  View folder [Ansible](https://github.com/PCharleigh/ElkProject/tree/main/Ansible) for playbooks.

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly reduntant, in addition to restricting unauthorized users to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box? 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system Logs.
- _TODO: What does Filebeat watch for? Filebeat monitors and watches the log files or locations that users specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing
- _TODO: What does Metricbeat record? Metricbeat Collect metrics from your systems and services. From CPU to memory, Redis to NGINX, and much more, It is a lightweight way to send system and service statistics.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| Web-1    | DVWA     | 10.0.0.5   | Linux            | 
| Web-2    | DVWA     | 10.0.0.6   | Linux            |
| Web-3    | DVWA     | 10.0.0.8   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Elk Server machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _TODO: 40.71.98.33

Machines within the network can only be accessed by the Jump Box Provisioner.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address? Only the Jump Box can access the Elk server and the ip address is 40.71.98.33

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | No                  | 66.46.55.146         |
| Elk Sever| Yes                 | 40.71.98.33          |
| Web-1    | No                  | 40.71.98.33          |
| Web-2    | No                  | 40.71.98.33          |
| Web-3    | No                  | 40.71.98.33          |


Connection to the Jump Box is accessed through port 22, as well as the Jump Box accessing the servers through port 22. The Jump Box can reach the Elk server because the two virtual networks are able to communicate through a peer connection. The dwva containers are can only be accessed through port 80. As for the Elk server, it allows all traffic in through port 5601. The Elk server is publically accessable because there were minimal security rules placed and it is not behind a load balancer unlike the other VM servers. 
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it saves time and reduces the chances of mistakes, especially when configuring multiple machines. 

The playbook implements the following tasks:
-Install docker.io
-Install python3-pip
-Install docker modules
-Increase virtual memory
-Download and launch docker elk container
-Enable sevrice docker on boot


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![docker ps](https://user-images.githubusercontent.com/100814056/156874705-9ed8a98c-c719-4413-a8c5-6140b592c5a7.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5
- 10.0.0.6
- 10.0.0.8

We have installed the following Beats on these machines:
- Metricbeat and Filebeat

These Beats allow us to collect the following information from each machine:
- Metricbeat collects metrics from the operating system and services running on the servers. Filebeat monitors and watches logs, then forwards the data to Elasticsearch or Logstash for indexing.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the .yml file to the ansible file.
- Update the host file to include the webservers
- Run the playbook, and navigate to the server website or use curl loclhost/setup.php to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it? The elk.yml file is the playbook located in the /etc/ansible file and you copy it to the ansible container.
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_ Update the host file when specifying which servers to run Filebeat on and input the ip address of the servers you wish to run Filebeat on.
- _Which URL do you navigate to in order to check that the ELK server is running? Open a new tab and input http://elk-ip:5601/app/kibana to confirm it is up and running

_Specific commands
-ansible-playbook *yml file*
-nano hosts to update webservers
-sudo docker ps
