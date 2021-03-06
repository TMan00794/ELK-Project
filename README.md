## Automated ELK Stack Deployment


![ELK-Diagram](Images/ELK_Diagram.png)

The files in this repository were used to configure the network depicted below.

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Playbook file may be used to install only certain pieces of it, such as Filebeat.

[Ansible Playbook](Ansible/ansible-playbook.yml)

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly stable, in addition to restricting traffic to the network.
- The primary function of a load balancer is to spread workloads across multiple servers to prevent overloading servers, optimize productivity and maximize uptime. Load balancing also provides the ability to add and remove instances without causing any disruption to incoming traffic.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log and system files.
- Filebeat will monitor the VMs by generating and organizing log files. Specifically, it logs information about the file system, including which files have changed and when
- Metricbeat will monitor the VMs by periodically collecting metrics from the operating system and from services running on the server.

The configuration details of each machine may be found below.

[Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables)

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
- <My_Public_IP>

Machines within the network can only be accessed by Jump-Box VM.
- 40.76.217.125

A summary of the access policies in place can be found in the table below.

| Name                | Publicly Accessible | Allowed IP Addresses     |
|---------------------|---------------------|--------------------------|
| Jump Box            | YES                 | <Public_IP_For_Jump-Box> |
| ELK-Server          | NO                  | 10.1.0.4                 |
| Web-1               | NO                  | 10.0.0.5                 |
| Web-2               | NO                  | 10.0.0.6                 |
| Web-3               | NO                  | 10.0.0.7                 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- We can use make updates to our server without disrupting incoming traffic. It is very simple to set up, no special coding skills are required for Ansible's playbooks, it is powerful by modeling highly complex IT workflows, and flexible by orchestrating the entire environment no matter where it is deployed.

The playbooks implement the following tasks:
- .Install docker
- .Install pip3
- .Install docker python module
- .Increased and set memory to 262144
- .Download and launch docker elk container:761  

[ELK Installation](Images/InstallingELK.PNG)

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

[Docker PS](Images/DockerPS.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 10.0.0.5
- Web-2 10.0.0.6
- Web-3 10.0.0.7
- Elk-Server 10.1.0.4

We have installed the following Beats on these machines:
- Filebeat  
- Metricbeat

These Beats allow us to collect the following information from each machine:

**FileBeat monitors and logs files or locations that you specify, to relay the information to Elasticsearch or Logstash for review

1. [Filebeat Configuration](Ansible/filebeat-configuratioin.yml)

2. [Filebeat Playbook](Ansible/filebeat-playbook.yml)

**Metricbeat records the metrics and statistics for uptime, and moves that information that you specify like Elasticsearch or Logstash

1. [Metricbeat Configuration](Ansible/metricbeat-config-file.yml)

2. [Metricbeat Playbook](Ansible/metricbeat-playbook.yml)

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:
- Copy the playbook file to /etc/ansible.
- Update the hosts file to include each VM Client IP address (10.0.0.5-10.0.0.7)
  - 10.0.0.5 ansible_python_interpreter=/usr/bin/python3
  - 10.0.0.6 ansible_python_interpreter=/usr/bin/python3
  - 10.0.0.7 ansible_python_interpreter=/usr/bin/python3
  - [elk]

[Hosts Configuration](Images/Hosts.PNG)

- Run the playbook, and navigate to 10.0.0.5 to check that the installation worked as expected.

- Run the playbook and navigateto 10.0.0.5 andcurl localhost/setup.php to check that the installation is running as expected.

- Check to make sure the ELK server is running:
  - Public IP on port 5601 (<My_VM'sPublic_IP>:5601/app/kibana#/home)
  - Kibana Application:


[Kibana](Images/Kibana.PNG)



## Downloading playbooks on your Machine


### Installing Filebeat on the DVWA Container
  - Navigate to http://[your.VM.IP]:5601/app/kibana. Use the public IP address of the ELK server that you created.
  - If you do not see the ELK server landing page, open a terminal on your computer and SSH into the ELK server.
  - Install Filebeat on your DVWA VM:
      - Open your ELK server homepage.
      - Click on Add Log Data.
      - Choose System Logs.
      - Click on the DEB tab under Getting Started to view the correct Linux Filebeat installation instructions.


### Creating the Filebeat Configuration File
  - Create a Filebeat configuration file and edit this file so that it has the correct settings to work with your ELK server.
  - Open a terminal and SSH into your jump box:
  - Start the Ansible container.
  - SSH into the Ansible container.
  - Copy the provided configuration file for Filebeat to your Ansible container: Filebeat Configuration File Template.
  - Note that when text is copy and pasted from the web into your terminal, formatting differences are likely to occur that will corrupt this configuration file.
  - Using curl is a better way to avoid errors and we have the file hosted for public download [HERE](Ansible/filebeat-configuration.yml)


### Setting up your Playbooks
  -  SSH into your Virtual machine using (ssh <Username_on_machine>@<IP_address_of_Machine>)
  -  Locate your container and making sure the container is running (docker container list -a)
          -if it isn't running: (docker start <name_of_your_machine>)
  -  After that you should be in your container if your username is (<root@<random_characters>:)
  -  Next 'cd' into your /etc/ansible directory.
  -  Install the .deb file using the dpkg command:
          - dpkg -i filebeat-7.4.0-amd64.deb1
  -  Run the 'filebeat modules enablesystem' command
  -  Run the 'filebeat setup' command
  -  Run the 'sevice filebeat start' command
  -  Run your command to start your installation of your playbook (ansible-playbook filebeat-playbook.yml)
  -  After this is done your playbook should be all set and ready to go!
