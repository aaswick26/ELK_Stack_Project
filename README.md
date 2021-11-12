## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

  - https://github.com/aaswick26/ELK_Stack_Project/blob/main/Diagrams/Cloud-Diagram_Elk_Stack.pdf

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Network Diagram file may be used to install only certain pieces of it, such as Filebeat.

  - https://github.com/aaswick26/ELK_Stack_Project/tree/main/Ansible

This document contains the following details:

  - Description of the Topology
  - Access Policies
  - ELK Configuration
    - Beats in Use
    - Machines Being Monitored
  - How to Use the Ansible Build

### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting high traffic to the network. Load balancers are also used to protect from DDos attacks by shifting attack traffic to the public cloud provider.

The jump box in this build adds significant security value because only one designated computer outside of the network is allowed access to a designated device within the network. This helps prevent others on the internet accessing the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system logs.

  - Filebeat watches for log files, collects them, and forwards them to Elasticsearch or Logstash.

  - Metricbeat records metric data from your system and services. i.e. CPU usage, memory, etc.

The configuration details of each machine may be found below.

| Name     | Function | IP Address                                    | Operating System |
|----------|----------|-----------------------------------------------|------------------|
| Jump Box | Gateway  | 10.0.0.9 (Private), 52.170.131.161 (Public)   | Linux            |
| ELK      | Server   | 10.1.0.4 (Private), 52.183.122.69 (Public)    | Linux            |
| Web-1    | Server   | 10.0.0.7 (Private)                            | Linux            |
| Web-2    | Server   | 10.0.0.8 (Private)                            | Linux            |
| Web-3    | Server   | 10.0.0.10 (Private)                           | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet.

Only the Jump-Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

  - My home Public IP Address

Machines within the network can only be accessed by SSH.

  - The only device allowed access to the ELK VM is my Home Public IP Address via port 5601.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses   |
|----------|---------------------|------------------------|
| Jump Box | Yes                 | Home Public IP Address |
| ELK      | No                  | Home Public IP Address |
| Web-1    | No                  | 10.0.0.9               |
| Web-2    | No                  | 10.0.0.9               |
| Web-3    | No                  | 10.0.0.9               |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

- Ansible is simple to setup and use.

The playbook implements the following tasks:

- Install Docker
- Install python3-pip
- Install Docker module pip
- Use systemctl to use more memory
- Download and launch Docker container sebp/elk:761

The following screenshot displays the result of running `docker ps -a` after successfully configuring the ELK instance.

  - https://github.com/aaswick26/ELK_Stack_Project/blob/main/Images/Elk_docker_ps.PNG

### Target Machines & Beats

This ELK server is configured to monitor the following machines:

  - Web-1 (10.0.0.7)
  - Web-2 (10.0.0.8)
  - Web-3 (10.0.0.10)

We have installed the following Beats on these machines:

  - Filebeat
  - Metricbeat

These Beats allow us to collect the following information from each machine:
  - Filebeat collects system logs, which can be used to track system events, etc.
  - Metricbeat collects system and service metric data, which we can use to see CPU usage, etc.

### Using the Playbook

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:
  - Copy the filebeat and metricbeat configuration files to /etc/ansible/directory_name/file_name.
  - Update the configuration files to include your ELK-server's private IP address.
  - Run the playbook, and navigate to http://[ELK-server-public-IP]:5601/app/kibana to check that the installation worked as expected.
