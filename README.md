# Elk-Stack-Project
A project demonstrating the configuration of an Elk stack server and set up of a cloud monitoring system.
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![alt text]


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Playbook file may be used to install only certain pieces of it, such as Filebeat.

  - [Ansible](https://docs.google.com/document/d/1mCb7aUuOvfHch5GpdM_j1hp8rsLu28_9/edit?usp=sharing&ouid=118229848406843865602&rtpof=true&sd=true)
  - [Filebeat](https://drive.google.com/file/d/1QC4391G81c8G_QwzwJl74dwQ0k7W6tnC/view?usp=sharing)
  - [Metricbeat](https://drive.google.com/file/d/1eQ3LT0SoB2boXY6TMBhsxP4b9MicGsiD/view?usp=sharing)
  - [Elk Installation](https://drive.google.com/file/d/1w5KT8HDggeuXbZGsFyNUsqVCQOO75OMw/view?usp=sharing)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network. Load balances protect the network system from a distributed denial of service (DDoS)attack by evenly distributing network traffic, preventing overload. The advantage of using a jump box is that it provides one access point where administrative task can be completed.  Access to a company network is obtained by using the jump box for SSH access. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
- Filebeat monitors and records the log files that have been indicated by the playbook.
- Metricbeat monitors the servers and collects metrics and statistical data from the operating system and other services running on the server.


The configuration details of each machine may be found below.


|     Name                         |     Function      |     IP Address    |     Operating System    |
|----------------------------------|-------------------|-------------------|-------------------------|
|     Jump Box                     |     Gateway       |     10.0.0.12     |     Linux               |
|     Web 1                        |     Webserver     |     10.0.0.13     |     Linux               |
|     Web 2                        |     Webserver     |     10.0.0.15     |     Linux               |
|     Web 3                        |     Webserver     |     10.0.0.5      |     Linux               |
|     Django-Elk-Stack   Server    |     Monitoring    |     10.1.0.4      |     Linux               |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: Personal Local IP address. 

Machines within the network can only be accessed by the Jump Box Provisioner. The Jump Box Provision is the only machine allowed to access the Elk-Stack server via ssh with the IP address (10.0.0.12). 

A summary of the access policies in place can be found in the table below.

|     Name                       |     Publicly Accessible    |     Allowed IP Addresses                                         |
|--------------------------------|----------------------------|------------------------------------------------------------------|
|     Jump Box                   |     Yes                    |     Local IP on   ssh port 22                                    |
|     Web-1                      |     No                     |     10.0.0.12 on   ssh port 22 and Local IP via Load Balancer    |
|     Web-2                      |     No                     |     10.0.0.12 on   ssh port 22 and Local IP via Load Balancer    |
|     Web-3                      |     No                     |     10.0.0.12 on   ssh port 22 and Local IP via Load Balancer    |
|     Django-Elk-Stack Server    |     No                     |     10.0.0.12 on   ssh port 22 and Local IP on TCP port 5601     |
|     Load Balancer              |     Yes                    |     Local IP on HTTP   port 80                                   |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because “automation with the docker frees up time and increases efficiency” (Arora,2021). 

The playbook implements the following tasks:

- Install Docker.io and pip3
- Increase VM Memory
- Download and Configure Elk docker container


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

! C:/Users/algr/OneDrive/Documents/Week 13/README/Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 10.0.0.13
- Web-2 10.0.0.15
   - Web-3 10.0.0.5

We have installed the following Beats on these machines:
- Filebeat
   - Metricbeat
 
These Beats allow us to collect the following information from each machine:
- Filebeats “collects log events and forwards them elastic search or Logstash for indexing” (fatalerrors.org).
   - Metricbeats collects “metric data from the target servers, such as CPU, memory, or data related to services running on the server” (Yadav, 2020).  
 
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml and the metricbeat-config.yml file to /etc/ansible/file.
- Update the configuration file to include the Private IP of the Elk-Server to the ElasticSearch and Kibana Sections of the Configuration File.
- Run the playbook,and navigate to http://13.77.68.49:5601/app/kibaba to check that the installation worked as expected.


### Additional Commands

|     COMMAND                                              |     PURPOSE                                              |
|----------------------------------------------------------|----------------------------------------------------------|
|     sudo apt-get   update                                |     Update all   packages                                |
|     sudo apt   install docker.io                         |     Install docker   application                         |
|     sustemctl status   docker                            |     Status of the   docker application                   |
|     sudo docker   pull cyberxsecurity/ansible            |     Downloads the   docker file                          |
|     sudo docker   run -ti cyberxsecurity/ansible bash    |     Run and create   a docker image                      |
|     sudo docker   start                                  |     Starts the   image specified                         |
|     sudo docker   ps -a                                  |     List all   active/inactive containers                |
|     sudo docker   attach                                 |     ssh into the ansible   container                     |
|     ssh-keygen                                           |     Create a ssh key                                     |
|     ansible -m   ping all                                |     Verify the   connection of all ansible containers    |


###Resources

- Arora, S. 2021. What is Ansible and How to Use Ansible Docker. Retrieved from https://www.simplilearn.com/tutorials/ansible-tutorial/what-is-ansible

- Understanding filebeat in an article.
https://www.fatalerrors.org/a/understanding-filebeat-in-an-article.html

- Yadav, V. 2020. Getting started with Metricbeats. Retrieved from 
https://medium.com/devops-dudes/getting-started-with-metricbeat-7c5718e6b3f4


