# ansible-raspberry-admin

**[Note]**
- xxxx

**[Pre requisite]**
- Raspberry Pi(s) with Raspbian

- Internet connectivity and IP address of the Raspberry Pi (get by scanner something like this : 
	1.sudo nmap -sn 192.168.1.0/24)

- Ansible (How to)


## 0 - Prepare Raspberry pi HostName

DO some stuff

## 1 - Install Ansible on Master pi

    sudo apt-get install python-pip git python-dev sshpass
    sudo pip install markupsafe
    sudo pip install ansible


## A - Share SSH key between remote hosts
First step : Set up a public/private keypair on the Raspberry pi controller so I don’t have to do any login stuff

    // Generate the key
    ssh-keygen -t rsa -b 4096 -f ~/.ssh/id_rsa
    // show it
    cat ~/.ssh/id_rsa.pub
    
Second step : Copy the key freshly output and use SSH to connect to each Pi from the raspberry pi Master

    ssh-copy-id pi@P1
    ssh-copy-id pi@P2
    ssh-copy-id pi@P3
    ssh-copy-id pi@P4

Not very efficient ...

The best solution

Create a file called 'servers'. One server by line.

    192.168.100.1
    server.example.com
    192.168.100.2
    server2.example.com
    
Create a script file

    #!/bin/bash
    
    for i in `cat servers`;
    do
       ssh-copy-id -i ~/.ssh/id_rsa.pub pi@$i
    done

## B - Project structure

    ./bootstrap.yml
    ./hosts
    ./keys/
    ./roles/
    
**Description**
    
- **bootstrap.yml** is an Ansible playbook that contains instructions about which roles are run on which hosts, and with which variables.
 
- **hosts** has a list of hosts where the configurations are run into.

- **keys** is a directory for SSH keys for passwordless access to the Raspberries.


   

## 1 - Configuring hosts

Create the hosts file and copy paste the data below

    [clusternodes]
    raspberrypi[1:4]
    [clusternodes:vars]
    ansible_ssh_user=pi


## 2 - Configuring ssh access

## 3 - Running script

    ansible-playbook -i hosts bootstrap.yml --ask-pass
    
On the first run to a fresh Raspbian you will ask to enter a new password
    
    $ ansible-playbook -i hosts bootstrap.yml --ask-pass
    SSH password:
    Enter new password for user pi:

    PLAY [all] *********************************************************************
    ...

## 4 - Test the devices modifications



**Sources:** 

    https://garthvh.com/blog/2017/02/11/Raspberry-Pi-Zero-Cluster-with-Ansible/
    http://www.hietala.org/automating-raspberry-pi-setup-with-ansible.html