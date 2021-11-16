# Elk-Cloud-Security-Project

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](diagrams/Azure%20Network%20Repository%20Project.jpg)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YML Playbook file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._

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
- _TODO: What aspect of security do load balancers protect?

- Load balancers protect the Availability, Web Traffic, and Web Security. Load balancers protect the machine from DDoS attacks by rerouting live traffic.

-   What is the advantage of a jump box?_

- The advantage of a jump box is that it allows automation, improves security, audits traffic of segmented networks, and allows for ease of access control by using a single point to be secured and monitored.

Integrating an ELK metrics and statistics server allows users to easily monitor the vulnerable VMs for changes to the logs files and system.

- _TODO: What does Filebeat watch for?_

- Filebeat monitors for any changes in information and when the changes took place.
- 
- _TODO: What does Metricbeat record?_

- Metricbeat records metrics and statistical data which is then sent out to a specified output: Elasticsearch or logistach for indexing.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| JumpBoxProvisioner | Gateway  | 10.0.0.4   | Linux            |
| Web-1     |Server   | 10.0.0.5   | Linux               |
| Web-2     |Server   | 10.0.0.6   |  Linux                |
| Web-ELK-1 | ELK Monitoring Server| 10.1.0.4  |  Linux  |
| load Balancer| Load Balancer | 20.115.30.252 | Linux |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBoxProvisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _TODO: Add whitelisted IP addresses_20.120.98.39.

Machines within the network can only be accessed by each other.
- _TODO: Which machine did you allow to access your ELK VM? 

- JumpBoxProvisioner

- What was its IP address?_

- Private IP: 10.0.0.4 via ssh on port 22


A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| JumpBoxProvisioner | Yes                             | 20.120.98.39 /10.0.0.4|
|  Web-1                       | No	                          | 10.0.0.5                       |
|  Web-2                       | No                              |  10.0.0.6                      |
| Web-ELK-1                | Yes                             | 52.165.18.54 /10.1.0.4| 
|Load Balancer            | Yes                              | 20.115.30.252


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_

- Ansible allows you to deploy multiple applications using a single    playbook.

- The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._

 ...Machine groups and remote user specifications:

- name: Configure Elk VM with Docker
  	  hosts: elk
  	  remote_user: azureuser
 	  become: true
  	  tasks:


- ...Increase system memory:

- name: Use more memory
      	  sysctl:
       	  name: vm.max_map_count
          value: "262144"
          state: present
          reload: yes

Install the following packages:


Docker.io
Python3-pip
Docker elk container
Launch docker container with these ports:


5601:5601
9200:9200
5044:5044


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](diagrams/Screenshot%20update%20path%20with%20names%20of%20docker%20ps%202021-11-16%20165313.png) 

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

- _TODO: List the IP addresses of the machines you are monitoring_
Web-1: 10.0.0.5
Web-2: 10.0.0.6

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_

Filebeat
Metricbeat

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

Filebeat is a lightweight shipper for forwarding and centralizing log data. Installed as an agent on your servers, Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.

Metricbeat is a lightweight shipper that you can install on your servers to periodically collect metrics from the operating system and from services running on the server. Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat playbook file to /etc/ansible.

![files](https://github.com/wildycapellan/Elk-Cloud-Security-Project/blob/main/diagrams/Screenshot%20filebeat%20playbook%20file%20to%20etc%20ansible%202021-11-16%20163620.png?raw=true)

- Update the /etc/ansible/hosts file to include Web-1, Web-2, and Web-ELK-1

![hosts](diagrams/Screenshot%20-%20Update%20the%20etc%20ansible%20hosts%20file%20to%20include%20Web-1%2C%20Web-2%2C%20and%20Web-ELK-1%20update%20t2021-11-16%20163833.png)

- Run the playbook, and navigate to hosts to check that the installation worked as expected.
![playbook](https://github.com/wildycapellan/Elk-Cloud-Security-Project/blob/main/diagrams/Screenshot%20Run%20the%20playbook,%20and%20navigate%20to%20hosts%20to%20check%20that%20the%20installation%20worked%20as%20expected%202021-11-16%20164143.png?raw=true)

![](https://github.com/wildycapellan/Elk-Cloud-Security-Project/blob/main/diagrams/Screenshot%20check%20that%20data%20is%20recevived%20from%20filebeat%202021-11-16%20164251.png?raw=true)

![](https://github.com/wildycapellan/Elk-Cloud-Security-Project/blob/main/diagrams/Screenshot%20filebeat%20dashboard%202021-11-16%20164417.png?raw=true)

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_

filebeat-playbook.yml the file was copy to /etc/ansible/playbooks.

- _Which file do you update to make Ansible run the playbook on a specific machine?

/etc/ansible/hosts file and add the IP address of the VM's under [webserver].

 How do I specify which machine to install the ELK server on versus which to install Filebeat on?_

 By specifying two groups in the /etc/ansible/hosts file, labeled [webservers] for filebeat, and [ELK] for Elk installation.


- _Which URL do you navigate to in order to check that the ELK server is running?

http://52.165.18.54:5601/app/kibana#/home


_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
