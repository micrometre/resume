---
title:  Ansible Events
publishDate: 2019-12-01 00:00:00
img: /assets/cloud_0.webp
img_alt: cloud computing image
description: Setting Up an Event-Driven System using Ansible Rulebook to Create and Configure Multipass VMs
tags:
  - Ansible
---



*In this blog post, we'll explore Ansible Rulebook to create an event-driven automation system for provisioning and configuring Multipass VMs. This approach allows you to automate VM creation and configuration based on triggered events.*
*By customizing the event triggers, Ansible roles, and playbook logic, you can create a robust and automated infrastructure management system.*
#### Prerequisites 
###### Ensure you have Multipass and Ansible installed on your Ubuntu or Debian system. 

- Ubuntu or Debian with Multipass <br/> 
Refer to the official documentation for installation instructions <br/>
<a href="https://canonical.com/multipass/install" target="_blank">
canonical.com Install Multipass  
 </a>


- To Ansible Install it following the official guide <br/>  

<a href="https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html" target="_blank">
Installing Ansible
</a>

##### Setting Up the Environment


###### Install Required Software:
```shell
sudo apt-get --assume-yes install openjdk-17-jdk python3-pip
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
export PATH=$PATH:~/.local/bin
pip3 install ansible ansible-rulebook ansible-runner
```
- Java (required by Ansible), 
- ansible: Core Ansible functionality.
- ansible-rulebook: Enables event-driven automation workflows.
- ansible-runner: Provides flexibility for running Ansible Playbooks.


##### Start the Ansible Rulebook Engine

```shell
ansible-rulebook --rulebook webhook-example.yml -i inventory/inventory.yml --verbose
```
###### This command starts the Ansible Rulebook engine, specifying:

```shell
# The path to the Ansible Rulebook definition file.
--rulebook webhook-example.yml: 
# The path to the inventory file defining target hosts.
-i inventory/inventory.yml: 
# Enables detailed output for debugging purposes.
--verbose: 
```
*Note: Replace webhook-example.yml and inventory/inventory.yml with the actual file paths for your setup.*

##### Triggering the Event (Example)



###### This curl command sends a POST request to the specified endpoint (127.0.0.1:5000/endpoint)

This command would trigger the execution Ansible playbook, 
automating VM creation and configuration.


```shell
curl -H 'Content-Type: application/json' -d "{\"message\": \"Create VM\"}" 127.0.0.1:5000/endpoint
```


##### List of Ansible Roles
- multipass: Creates Multipass VMs.
- common: Updates and upgrades the system, installs required packages.
- users: Creates a new user with sudo privileges, sets up SSH keys, and grants passwordless sudo access.
- docker: Installs Docker and the docker-compose-plugin.
- nodejs: Installs Node Version Manager (NVM) and Node.js.`

###### Code Repository <a href="https://github.com/micrometre/ansible-events">https://github.com/micrometre/ansible-events </a>