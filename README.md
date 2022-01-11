## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![ELK Stack Diagram](https://github.com/natyhi/ELK-Stack-project/blob/main/ELK%20Diagram/Cloud%20Security.drawio.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ANSIBLE file may be used to install only certain pieces of it, such as Filebeat.

  [Ansible](https://github.com/natyhi/ELK-Stack-project/tree/main/Ansible)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly secured, in addition to restricting unauthorized network traffic to the network.
-The off-loading function of a load balancer defends an organization against distributed denial-of-service (DDoS) attacks. The advanatge is that admin can jump into a secure computer before they start an administrative task or to connect to a untrusted enviroments.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
-File beat watches for forwarding and centralizing log data.
- Metricbeat takes the metrics and stats that it collects and ships them to the output.

The configuration details of each machine may be found below.

| Name     | Function                                              | IP Address   | Operation System |
|----------|-------------------------------------------------------|--------------|------------------|
| Jump-Box | To connect to different VM's with only one port.      | 20.120.16.53 | Linux            |
| Web-1    | PHP/SQL web application to aid security professionals | 10.0.0.5     | Linux            |
| Web-2    | PHP/SQL web application to aid security professionals | 10.0.0.6     | Linux            |
| ElK      | The ability to aggregate logs from all systems        | 10.1.0.4     | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JUMPBOX machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- PORT 5601

Machines within the network can only be accessed by JUMPBOX.
- Which machine did you allow to access your ELK VM? JUMPBOX.  IP address 10.0.0.7.

A summary of the access policies in place can be found in the table below.

| Name     | Public Accessible  | Allowed IP Address |
|----------|--------------------|--------------------|
| Jump-Box | Yes                | 20.120.16.53       |
| Web-1    | No                 | 10.0.0.5/10.0.0.7  |
| Web-2    | No                 | 10.0.0.6/10.0.0.7  |
| ElK      | Yes                | 20.120.16.53/10.0.0.7    |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- It will help with the representation of Infrastructure (IAC) also, you don't need speacialized coding skills to set it up. 

The playbook implements the following tasks:
- install docker and ansible within a jumpbox run the playbook to enable the filebeat/metric software to other servers.
- Added Elk Vm to jumpbox seperate container and under the ELK group name
- ran the ansible-playbook command to start all
- Used commnad docker ps -a to obtain docker and then ran docker start and attach with my container name. 
- ...

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![image](https://user-images.githubusercontent.com/70927264/148159282-de00985d-1f47-4a07-bb4b-1d7f41f94590.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Both Web-1 & 2 are being monitored 10.0.0.5/10.0.0.6

We have installed the following Beats on these machines:
-Filebeat and Metricbeat have been installed.

These Beats allow us to collect the following information from each machine:
- Filebeat is used to collect logs from specific files on a remote enviorment an example is the Apache which can generate filebeat request/responses.
- Metricbeat collects metrics to anaylze for the health of the VM an  example would be CPU's usage

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook.yml file to etc/ansible/roles/files.
- Update the Ansibleconfig file to include WEB servers ip and ELK IP addressess
- Run the playbook, and navigate to Kibana to check that the installation worked as expected.

Which file is the playbook? Where do you copy it?
- _The playbook file should be located in the ansible directory under playbook.yml. Where do you copy it, i copied it from the playbook.yml file.
- _Which file do you update to make Ansible run the playbook on a specific machine? I update the/etc/ansible/hosts.
-  How do I specify which machine to install the ELK server on versus which to install Filebeat on? I updated the ansible configuration file to denote the Web servers and ELK vm
- _Which URL do you navigate to in order to check that the ELK server is running? this is the url http://40.122.238.253:5601/

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
1.Make sure your AZURE VMs are up and running.
2.As a user the first command install playbook.yml
3.On the terminal SSH into jumpbox.
4.then run the docker sudo commands ( sudo -i, sudo docker ps -a, sudo start docker 'name of docker', sudo attach docker 'name of docker')
5. Once in the root of your container run your either beat from the container you are in. by using command ansible-playbook. You can use anisble-playbook to run your playbook and also your beats. 
