# ansible-raspberry-admin

**[Note]**
- xxxx

**[Pre requisite]**
- Raspberry Pi(s) with Raspbian

- Internet connectivity and IP address of the Raspberry Pi (get by scanner something like this : 
	1.sudo nmap -sn 192.168.1.0/24)

- •Ansible (Installation instructions)

- •Clone of raspberry-ansible repository




## 0 - Prepare Raspberry pi HostName

DO some stuff


## A - Share SSH key between remote hosts
First i set up a public/private keypair on the Raspberry pi controller so I don’t have to do any login stuff

    // Generate the key
    ssh-keygen -t rsa -b 4096 -f ~/.ssh/id_rsa
    // Spit it Out
    cat ~/.ssh/id_rsa.pub
    
Second copy the key freshly output and used SSH to connect to each Pi Zero from the raspberry pi controller

    sudo ssh pi@P1, P2, P2, P4
    sudo mkdir ~/.ssh
    sudo nano ~/.ssh/authorized_keys

Need to Paste Precedently key copied ... Not very efficient ...

ssh-copy-id pi@P1
ssh-copy-id pi@P2
ssh-copy-id pi@P3
ssh-copy-id pi@P4

Not very efficient to...

The best solution

Create a file called servers. On server by line

    192.168.100.1
    server.example.com
    192.168.100.2
    server2.example.com
    
Create a script file

    for i in `cat servers`;
    do
       ssh-copy-id -i ~/.ssh/id_rsa.pub pi@$i
    done

## B - 
