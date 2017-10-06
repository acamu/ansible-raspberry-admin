# ansible-raspberry-admin

**[Note]**
- xxxx

**[Pre requisite]**
- Ansible


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

## B - 
