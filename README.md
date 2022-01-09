

ELK Stack Deployment Project
==============================
The files in this repository were used to configure the network depicted below.  

![Network Diagram](/Diagrams/Cloud-Security-and_ELK-Stack-Deployment-Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the **_yml and config_** file may be used to install only certain pieces of it, such as Filebeat.

* [My First Playbook](/Ansible/Docker/pentest.yml "My First Playbook")
* [Ansible ELK Installation and VM Configuration](/Ansible/ELK-Stack/install-elk.yml "Ansible ELK Install and VM Config")
* [Hosts File](/Ansible/ELK-Stack/hosts "Hosts")
* [Ansible Configuration](/Ansible/ELK-Stack/ansible.cfg "Ansible Configuration")
* [Filebeat Config](/Ansible/Filebeat/filebeat-config.yml "Filebeat Config")
* [Filebeat Playbook](/Ansible/Filebeat/filebeat_playbook.yml "Filebeat Playbook")
* [Metricbeat Config](/Ansible/Metricbeat/metricbeat-config.yml "Metricbeat Config")
* [Metricbeat Playbook](/Ansible/Metricbeat/metricbeat-playbook.yml "Metricbeat Playbook")

This document contains the following details:

- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build

-------------------------------------------------------------------------------------------------------------------------------------------

### **Description of the Topology**  

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly **_functional and available_**, in addition to restricting **_traffic_** to the network.

**Question: What aspect of security do load balancers protect?**

Answer: Load balancers add redunancy aand resilence by rerouting live traffic from one server to another if a server falls victim to an attack or otherwise becomes unavailable.

**Question: What is the advantage of a jump box?**
  
Answer: A Jump Box Provisioner is an important virtual macchine as it prevents Azure VMs from being exposed via a public IP Address. Allowing us to monitor and log on a single machine. IP addresses can also be restricted to communicate with the Jump Box to further add protection, as demonstrated in the ELK Stalk Deployment.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the **_network_** and system **_system logs_**.

**Question: What does Filebeat watch for?**

Answer: Filebeat monitors the log files or locations that you specify, collecting log events, forwarding them either to Elasticsearch or Logstash for indexing.
 
**Question: What does Metricbeat record?**

Answer: Metricbeat takes metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.

-------

### **The configuration details of each machine may be found below.**


| Name              | Function        | IP Address               | Operating System   |
|-------------------|-----------------|--------------------------|--------------------|
| Jump Box          | Gateway         | 10.1.0.4 / 20.211.171.98  | Linux              |
| Web-1             | UbuntuServer    | 10.1.0.5 / 20.53.224.117 | Linux              |
| Web-2             | UbuntuServer    | 10.1.0.6 / 20.53.224.117 | Linux              |
| ELKserver         | UbuntuServer    | 10.2.0.5 | Linux              |

-----------------------------------------------------------------

## **Access Policies**  

The machines on the internal network are not exposed to the public Internet.

Only the **_Jump-Box-Provisioner_** machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

**_Workstation using my Public IP through TCP 5601._**

Machines within the network can only be accessed by **_Workstation and Jump-Box-Provisioner through SSH Jump-Box._**

**Question:  Which machine did you allow to access your ELK VM?**

Answer: Jump-Box-Provisioner IP : 10.1.0.4 via SSH port 22

**Question: What was its IP address?**

Answer: Workstation using my Public IP via port TCP 5601.

A summary of the access policies in place can be found in the table below.
|        Name        |  Publicly Accessible  |          Allowed IP Addresses           |
|--------------------|-----------------------|-----------------------------------------|
| Jump Box           | Yes                   | Workstation IP on SSH 22)               |
| Web-1              | No                    | 10.1.0.5 on SSH 22                      |
| Web-2              | No                    | 10.1.0.6 on SSH 22                      |
| ELKserver          | Yes                   | http://your-elk-vm-ip:5601              |

-------------------------------------------------------------------------------------------------------------------------------------------

## **Elk Configuration**  
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because.

**Question: What is the main advantage of automating configuration with Ansible?**
Answer: Ansible allows you quickly and easily deploy multitier applications through a YAML playbook. You don't need to write custom code to automate systems.

The playbook implements the following tasks:

**In 3-5 bullets, explain the steps of the ELK installation**

  - Specify a different group of machines
  - Install Docker.io
  - Install Python-pip
  - Install Docker module
  - Increase Virtual Memory
  - Download and Launch ELK Docker Container (image sebp/elk)
  - Published ports 5044, 5601 and 9200 were made available

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.  

ELKserver
---------
![DockerPS](/Images/Sudo-Docker-Container-List-ELK.png "ELKserver")

Jump-Box-Provisioner
--------------------
![DockerPS](/Images/Sudo-Docker-Container-List.png "Jump-Box-Provisioner")

-------------------------------------------------------------------------------------------------------------------------------------------

## **Target Machines & Beats**
This ELK server is configured to monitor the following machines:

- List the IP addresses of the machines you are monitoring
  - Web-1: 10.1.0.5
  - Web-2: 10.1.0.6
 
We have installed the following Beats on these machines:

Filebeat
---------
![Filebeat Status Screenshot](/Images/Filebeat-success-data.png "Filebeat Data Successful")

Metricbeat
----------
![Metricbeat Status Screenshot](/Images/Metricbeat-success-data.png "Metricbeat Data Successful")

These Beats allow us to collect the following information from each machine:

  - Filebeat will be used to collect log files from very specific files such as Apache, Microsft Azure tools and web servers, MySQL databases.

  - Metricbeat will be used to monitor VM stats, per CPU core stats, per filesystem stats, memory stats and network stats.

## Using the Playbook  
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

- Verify the Public IP address to see if it has changed. [What Is My IP?](https://www.whatismyip.com/)
- If changed then update the Security Rules that uses the My Public IPv4

SSH into the control node and follow the steps below:

- Copy the **_yml_** file to **_ansible folder._**
- Update the **_config_** file to include **_remote users and ports._**
- Run the playbook, and navigate to **_Kibana Your IP Address:5601_** to check that the installation worked as expected.

## Answer the following questions to fill in the blanks:*

**Question: Which file is the playbook?**

Ansible: [My First Playbook](/Ansible/Docker/pentest.yml "My First Playbook")

Filebeat: [Filebeat Playbook](/Ansible/Filebeat/filebeat_playbook.yml "Filebeat Playbook")

Metricbeat: [Metricbeat Playbook](/Ansible/Metricbeat/metricbeat-playbook.yml "Metricbeat Playbook")

**Question: Where do you copy it?**

_/etc/ansible/_

**Question: Which file do you update to make Ansible run the playbook on a specific machine?**

_/etc/ansible/hosts file (IP of the Virtual Machines).  

**Question: How do I specify which machine to install the ELK server on versus which to install Filebeat on?**
  
I have specified two separate groups in the etc/ansible/hosts file. One of the group will be webservers which has the IPs of the 2 VMs that I will installed Filebeat to. The other group is named ELKserver which will have the IP of the VM I have installed ELK to.  

**Question:Which URL do you navigate to in order to check that the ELK server is running?**

http://20.84.136.248:5601/app/kibana

-------------------------------------------------------------------------------------------------------------------------------------------

As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc.  

|            COMMAND                               | PURPOSE                                               |
|--------------------------------------------------|-------------------------------------------------------|                         
|`ssh-keygen`                                      |  create a ssh key for setup VM's                      |
|`sudo cat .ssh/id_rsa.pub`                        |  to view the ssh public key                           |
|`ssh azureadmin@Jump-Box-Provisioner IP address`     |  to log into the Jump-Box-Provisioner                 |
| `sudo docker container list -a`                  | list all docker containers                            |
| `sudo docker start gifted_kapitsa`               | start docker container gifted_kapitsa                |
|`sudo docker ps -a`                               |  list all active/inactive containers                  |
|`sudo docker attach gifted_kapitsa`               |  effectively sshing into the gifted_kapitsa  container |
|`cd /etc/ansible`                                 | Change directory to the Ansible directory             |
|`ls -a`                                         | List all file in directory (including hidden)         |
|`nano /etc/ansible/hosts`                         |  to edit the hosts file                               |
|`nano /etc/ansible/ansible.cfg`                   |  to edit the ansible.cfg file                         |
|`nano /etc/ansible/pentest.yml`                   |  to edit the My-Playbook                              |
|`ansible-playbook [location][filename]`           |  to run the playbook                                  |
|`ssh azureuser@Web-1 IP address`                    |  to log into the Web-1 VM                             |
|`ssh azureuser@Web-2 IP address`                    |  to log into the Web-2 VM                             |
|`ssh azureuser@ELKserver IP address`                |  to log into the ELKserver VM                         |
|`exit`                                            | to exit out of docker containers|
|`nano /etc/ansible/ansible.cfg`                   |  to edit the ansible.cfg file                         |
|`nano /etc/ansible/hosts`                         |  to edit the hosts file                               |
|`nano /etc/ansible/pentest.yml`                   |  to edit the My-Playbook                              |
|`ansible-playbook [location][filename]`           |  to run the playbook                                  |
|`sudo apt-get update` 				                     |  this will update all packages                        |
|`sudo apt install docker.io`				               |  install docker application		                       |
|`sudo service docker start`				               |  start the docker application                         |
|`sudo systemctl status docker`				             |  status of the docker application                     |
|`sudo systemctl start docker`                     |  start the docker service                             |
|`sudo docker pull cyberxsecurity/ansible`	       |  pull the docker container file                       |
|`sudo docker run -ti cyberxsecurity/ansible bash` |  run and create a docker container image              |
|`ansible -m ping all`                             |  check the connection of ansible containers           |
|`dpkg -i [filename]`                              |  to install the file i.e. (filebeat & metricbeat)     |
|`http://20.53.224.117/:5601//app/kibana`           | Open web browser and navigate to Kibana Logs          |
|`nano filebeat-config.yml`                        | create and edit filebeat config file                  |
|`nano filebeat-playbook.yml`                      | write YAML file to install filebeat on webservers     |
|`nano metricbeat-config.yml`                      | create metricbeat config file and edit it             |
|`nano metricbeat-playbook.yml`                    | write YAML file to install metricbeat on webservers   |  
-----------------------------------------------------------------------------------------------------------