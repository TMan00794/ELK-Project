## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![ELK-Diagram](Images/ELK_Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Playbook file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly _____, in addition to restricting _____ to the network.
- The primary function of a load balancer is to spread workloads across multiple servers to prevent overloading servers, optimize productivityand maximize uptime. Load balancing also provides the ability to addl and remove instances without causing any disruption to incoming traffic.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _____ and system _____.
- Filebeat will monitor the VMs by generating and organizing log files. Specifically, it logs information about the file system, including which files have changed and when
- Metricbeat will monitor the VMs by periodically collecting metrics from the operating system and from services running on the server.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name       | Function | IP Address | Operating System |
|----------  |----------|------------|------------------|
| Jump Box   | Gateway  | 10.0.0.1   | Linux            |
| Web-1      | Client   | 10.0.0.5   | Linux            |
| Web-2      | Client   | 10.0.0.6   | Linux            |
| Web-3      | Client   | 10.0.0.7   | Linux            |
| ELK-Server | Gateway  | 10.1.0.4   | Linux            |


### Access Policies

The machines on the internal network are not exposed to the public Internet.

Only the Jump-Box Machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 216.26.121.101

Machines within the network can only be accessed by _____.
- 40.76.217.125

A summary of the access policies in place can be found in the table below.

| Name                | Publicly Accessible | Allowed IP Addresses |
|---------------------|---------------------|----------------------|
| Jump Box            | Yes/No              | 10.0.0.1 10.0.0.2    |
| /images/SSHAccess   |                     |                      |
| /Images/Jump-Box-ip |                     |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- We can use make updates to our server without disrupting incoming traffic. It is very simple to set up, no special coding skills are required for Ansible's playbooks, it is powerful by modeling highly complex IT workflows, and flexible by orchestrating the entire environment no matter where it is deployed.

The playbooks implement the following tasks:
- .Install docker
- .Install pip3
- .Install docker python module
- .Increased and set memory to 262144
- .Download and launch docker elk container:761  

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 10.0.0.5
- Web-2 10.0.0.6
- Web-3 10.0.0.7
- Elk-Server 10.1.0.4 /Images/Network Interfaces

We have installed the following Beats on these machines:
- Filebeat  
- Metricbeat
 -delete me

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:
- Copy the playbook file to /etc/ansible.
- Update the hosts file to include each VM Client IP address (10.0.0.5-10.0.0.7)
- Run the playbook, and navigate to 10.0.0.5 to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
