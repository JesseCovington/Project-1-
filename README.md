# Project-1
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Virtual Network Diagram](c/Users/jessi/Project-1-/Diagrams/VNW_diagram.drawio.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select playbook files may be used to install only certain pieces of it, such as Filebeat.

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

Load balancing ensures that the application will be highly stable, in addition to restricting access to the network.
- Load Balancers protect from DDoS attacks as web traffic is directed to different machines. 
- The advantage of using a Jump box in this network means that updating or changing the webserver machines on this network can be done simultaniously while restricting access to the network to a single gateway. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
- Filebeat monitors logs files and changes to log events.
- Metricbeat collects metrics form the system and services running on the server.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| P1Emanager     | ELK host  | 10.1.0.4   | Linux           |
| Web1     | DVWA webserver  | 10.0.0.5   | Linux           |
| Web2     | DVWA webserver  | 10.0.0.6   | Linux           |
| Web3     | DVWA webserver  | 10.0.0.7   | Linux           |

### Access Policies

The machines on the internal network are not exposed to the public Internet.

Only the "JumpBoxProvisioner" machine can accept connections from the Internet. Access to this machine is only allowed from the following IP address:
172.73.160.144

Machines within the network can only be accessed by the "JumpBoxProvisioner".
- The ELK host VM can only be reached from 10.0.0.1, the "JumpBoxProvisioner" VM.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| JumpBoxProvisioner | Yes       | 172.73.160.144       |
| P1Emanager | No                | 10.0.0.1             |
| Web1     | No                  | 10.0.0.1, 10.0.0.6, 10.0.0.7, 10.1.0.4   |
| Web2     | No                  | 10.0.0.1, 10.0.0.5, 10.0.0.7, 10.1.0.4   |
| Web3     | No                  | 10.0.0.1, 10.0.0.5, 10.0.0.6, 10.1.0.4   |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- All recieving machines are updated simultaniously.
- Each machine recieves the exact same update.
- Human error is minimized and contained to the initial Ansible playbook. This saves time as the Ansible playbook can be corrected once and fix any number of recieving machines.

The playbook implements the following tasks:
- Installs Docker
- Installs python3_pip
- Installs the Docker Module
- Runs the following command: sysctl -w vm.max_map_count=262144
- Download and Launch a Docker Container: ELK
- Enables docker on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5, "Web1"
- 10.0.0.6, "Web2"
- 10.0.0.7, "Web3"

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat will collect changes made to our logs.
- Metricbeat will collect statistics and metrics of our network.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:
- Copy the filebeat-playbook.yml file to etc/ansible/roles/filebeat-playbook.yml.
- Copy the install-elk.yml file to etc/ansible/roles/install-elk.yml
- Update the hosts file to include the different groups of servers. Then specify which group will get filebeat installed: _webservers_ in the filebeat-playbook.yml and which server will get ELK installed in the install-elk.yml with the correct group: _elk_.
- Run the playbook, and navigate to http://40.113.244.59:5601/app/kibana to check that the installation worked as expected.

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
