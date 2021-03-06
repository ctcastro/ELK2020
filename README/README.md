## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Network Diagram](https://github.com/ctcastro/ELK2020/blob/master/README/Resources/Images/diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the [ELKSTACKSETUP.rtf)](https://github.com/ctcastro/ELK2020/blob/master/README/Resources/Scripts/ELKSTACKSETUP.rtf) file may be used to install only certain pieces of it, such as Filebeat.

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly responsive, in addition to restricting downtime of the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system metrics.

The configuration details of each machine may be found below.

| Name     | Function            | IP Address | Operating System |
|----------|---------------------|------------|------------------|
| Jump Box | Gateway             | 10.0.0.5   | Linux            |
| ELK VM   | Host ELK Stack      | 10.0.0.8.  | Linux            |
| DVWA-VM1 | Host DVWA Container | 10.0.0.6   | Linux            |
| DVWA-VM2 | Host DVWA Container | deleted    | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- HomePublicIP

Machines within the network can only be accessed by the Jump Box (10.0.0.6).

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | No                  | HomePublicIP         |
| ELK VM   | No                  | HomePublicIP         |
| DVWA-VM1 | No                  | 10.0.0.6             |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it provides an autonomous delivery which removes any discrepencies caused by human error aswell as saves time which can be used to perform other tasks.

The playbook implements the following tasks:
- Configure DVWA virtual machines with Docker, Pip, Python Module and the DVWA web container.
- Configures ELK Server with Docker, Pip, Python and the ELK container with Kibana.
- Installs and configures Filebeat to run within Kibana.
- Installs and configures Metricbeat to run within Kibana. 

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![ELK Command](https://github.com/ctcastro/ELK2020/blob/master/README/Resources/Images/Screen%20Shot%202020-06-03%20at%208.05.27%20PM.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
| Name     | IP Address |
|----------|------------|
| DVWA-VM1 | 10.0.0.6   |
| DVWA-VM2 | DELETED    |

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat collects and parses logs created by the system logging service in order to easily monitor the server(s).
- Metricbeat collects metrics from your systems and services, which we can use to make sure system functions are performing as expected and not utilizing too many resources.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the [ELKSTACKSETUP.rtf](https://github.com/ctcastro/ELK2020/blob/master/README/Resources/Scripts/ELKSTACKSETUP.rtf) file to "/etc/ansible/".
- Copy the [Metricbeat_config.rtf](https://github.com/ctcastro/ELK2020/blob/master/README/Resources/Scripts/metricbeat_config.rtf) file to "/etc/ansible/".
  - EDIT "10.0.0.6" on line 46 & 70 to the internal IP of your ELK server.
- Copy the [Filebeat_config.rtf](https://github.com/ctcastro/ELK2020/blob/master/README/Resources/Scripts/Filebeat_config.rtf) file to "/etc/ansible/".
  - EDIT "10.0.0.6" on line 1105 & 1804 to the internal IP of your ELK server.
- Update the "/etc/ansible/hosts" file to include the internal IPs of your "Webservers" and your "Elkserver".
- Run the playbook, and navigate to "PublicIPofELKServer:5601" to check that the installation worked as expected.

### Commands To Initialize Software
- ssh username@JumpboxIP
- sudo docker container start containername
- sudo docker container attach containername
  - ssh username@DVWA-VM1
    - exit
  - ssh username@DVWA-VM2
    - exit
  - ssh username@ELKServer
    -exit
  - cd /etc/ansible
  - ansible-playbook [ELKSTACKSETUP.rtf](https://github.com/ctcastro/ELK2020/blob/master/README/Resources/Scripts/ELKSTACKSETUP.rtf)

After completing all of these commands aswell as the instructions from "Using the Playbook" you should have a fully functional ELK Stack.

*note* these .rtf files seem to code the .yml text. Im able on my end to quickly find the correct text but it seems im having trouble downloading it as .yml
