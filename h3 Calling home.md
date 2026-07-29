# h3 Calling home


## Summary
### Two Machine Virtual Network With Debian 11 Bullseye and Vagrant

- The purpose of Vagrant is to automate the installation of virtual machines and SSH login entirely without a graphical user         interface. 
- 11-bullseye is no longer used, but rather debian/bookworm64. (Tero Karvinen 2021)

### Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux

- In Salt, one master server can manage multiple minion servers.
- The minion's configuration file defines the master's IP address and id. The master accepts the minion's keys, after which the master can run commands on all minion machines. (Tero Karvinen 2018)

### Salt Vagrant - automatically provision one master and two slaves

- In Salt, infrastructure is defined as states in text files.
- top.sls defines which states are run on which machines. (Tero Karvinen 2023)


## Installing Vagrant

I started by installing Vagrant. (Vagrant)
I installed AMD64 (Version: 2.4.9) on my machine. Once the installation was complete, I restarted my computer. 
After this, I tested with the command vagrant --version that Vagrant had been installed on my Windows host machine.
I had already previously installed the VirtualBox needed for this task on my computer. 
 
<img width="503" height="105" alt="image" src="https://github.com/user-attachments/assets/9ec8d4e5-565a-4747-b4fb-7679f4908791" />

## New Linux Virtual Machine

I first created the folder vagrant-test.

<img width="617" height="217" alt="image" src="https://github.com/user-attachments/assets/8c995c06-d3aa-4ba2-962b-b3dd89e7f241" />

I created the Vagrant file with the command vagrant init --minimal debian/bookworm64, after which I started the virtual machine with the command vagrant up.

<img width="886" height="220" alt="image" src="https://github.com/user-attachments/assets/f10bada4-05b4-489d-9d60-ef6b4253a2dc" />

I logged into the machine via SSH connection.
<img width="995" height="231" alt="image" src="https://github.com/user-attachments/assets/606684c5-4a21-4099-9dfb-03ae7bce65d8" />

I checked which Linux version was running on the VM. (Gcore 2023)
<img width="828" height="208" alt="image" src="https://github.com/user-attachments/assets/63b91f33-0833-4d0d-9934-12f0755cc7b8" />

I also tested with the command vagrant status that the virtual machine was up.
<img width="974" height="256" alt="image" src="https://github.com/user-attachments/assets/4345a897-339f-4413-903a-0850b000bacd" />


## Two Linux Computers Network with Vagrant

This task follows the instructions of (Tero Karvinen 2021), adapted for Windows.

I created a new folder called twohost with the command mkdir twohost and moved into that folder with cd twohost.
Next, I opened the Vagrantfile for editing with the command notepad vagrantfile, and pasted in the necessary script.
After saving the file, I started both virtual machines with the command vagrant up t001 t002.

<img width="897" height="370" alt="image" src="https://github.com/user-attachments/assets/8b7ab7f7-1b7e-47ae-b54a-0116ff0ebb7c" />

I ran the command vagrant status, which showed that both machines were running and the installation had succeeded.

<img width="993" height="291" alt="image" src="https://github.com/user-attachments/assets/c965f16b-42ca-4a17-9057-2b7342d69626" />

I established an SSH connection to t001 with the command vagrant ssh t001, after which I pinged the other machine I had created, t002, with the command ping -c 1 192.168.88.102.

<img width="996" height="390" alt="image" src="https://github.com/user-attachments/assets/34f52d1b-3a4e-4cce-b33e-c6f740c65cb6" />

I exited the SSH connection to t001 with exit, after which I tried pinging t001 from t002 in turn. That also succeeded.

<img width="988" height="402" alt="image" src="https://github.com/user-attachments/assets/13fc2f54-9e88-4377-9b63-962637a6a84a" />

I also tested the connection to the Internet, and that succeeded too. 

<img width="903" height="206" alt="image" src="https://github.com/user-attachments/assets/3b6a6f92-5dae-489f-b1c5-23ecd79c1bf1" />

## Salt Master Installation

This task follows the instructions of (Tero Karvinen 2018).

I ran the command vagrant up, after which I established an SSH connection to t001.
I created the keyrings folder with the command mkdir -p /etc/apt/keyrings.
I ran the command sudo apt-get update, after which I installed curl with the command sudo apt-get install curl.

<img width="1004" height="68" alt="image" src="https://github.com/user-attachments/assets/be0238a7-a88b-4c10-80ae-8b725445989e" />

I added Salt's package repository to APT's source list.

<img width="958" height="69" alt="image" src="https://github.com/user-attachments/assets/68f2ede0-5eff-4006-a77a-0e24ab1f8efc" /> (Salt project.io 2024)

Next, I ran the command sudo apt-get update, after which I installed salt-master with the command sudo apt-get -y install salt-master.

<img width="969" height="492" alt="image" src="https://github.com/user-attachments/assets/adc658df-ac3b-4166-aa6d-d1aa9c776c2b" />

It succeeded.  

## Salt Minion Installation

This task follows the instructions of (Tero Karvinen 2018).

I established an SSH connection to t002. I ran the command sudo apt-get update, after which I installed curl with the command sudo apt-get install curl. 
Next, I created the keyrings folder with the command mkdir -p /etc/apt/keyrings. 
Then I downloaded and added the public key with the following command:

<img width="1004" height="48" alt="image" src="https://github.com/user-attachments/assets/75cdce5a-2fd7-4b84-99bf-8901746a7058" />

I added Salt's package repository to APT's source list.

<img width="1004" height="128" alt="image" src="https://github.com/user-attachments/assets/16331741-7ec1-4419-af2b-5c3a9440d97a" /> (Salt project.io 2024)

Next, I ran the command sudo apt-get update, after which I installed salt-minion with the command sudo apt-get -y install salt-minion.

<img width="969" height="778" alt="image" src="https://github.com/user-attachments/assets/7a7b584a-ead6-4758-b16b-2e84e3c82b08" />

It succeeded.

<img width="969" height="778" alt="image" src="https://github.com/user-attachments/assets/17445fb4-0c0c-4508-9f3d-8fe45d47d2c9" />

Next, I ran the command sudoedit /etc/salt/minion, which opened Salt's configuration file for me. I edited the section #master: salt in the file. I changed it to look like this:

<img width="1004" height="643" alt="image" src="https://github.com/user-attachments/assets/3eb3f141-ce87-4119-954f-c59227a6c917" />

I saved the changes and restarted the minion with the command sudo systemctl restart salt-minion.
I also checked the minion's status as follows:

<img width="1004" height="363" alt="image" src="https://github.com/user-attachments/assets/8f7a8ee5-fdc3-45fb-b835-d1c7b0563ba2" />

Next, I returned to the master (t001) to accept the key.

<img width="695" height="209" alt="image" src="https://github.com/user-attachments/assets/6a584467-7bca-41e2-8bde-ba949c56d8b0" />

I tried the following command and received a response from the minion.

<img width="695" height="125" alt="image" src="https://github.com/user-attachments/assets/ae601539-6c60-454e-86ef-9159582609ec" />

## pkg and service over the network

I installed the packages tree and apache2 on the minion using the commands shown in the following images.

<img width="920" height="711" alt="image" src="https://github.com/user-attachments/assets/176d5263-ca96-449a-85bc-6828a08dbdcd" />
<img width="1004" height="36" alt="image" src="https://github.com/user-attachments/assets/d6455553-c95c-4b2c-affd-e56ac9eb4d58" />
<img width="538" height="219" alt="image" src="https://github.com/user-attachments/assets/c4144dee-69c1-4731-b2b9-f6e7e07e31a5" />

I used the command shown in the following image to verify that Apache was running and would start on boot.

<img width="1004" height="444" alt="image" src="https://github.com/user-attachments/assets/63682162-bfb4-45d1-98aa-9f5be9ee911f" />


## Sources

Karvinen, T. 28 March 2023. URL: https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file.

Karvinen, T. 28 March 2018. URL: https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/?fromSearch=salt%20quickstart%20salt%20stack%20master%20and%20slave%20on%20ubuntu%20linux. 

Karvinen, T. 11 April 2021. URL: https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/.

Saltproject.io. 28 October 2024. URL: https://saltproject.io/blog/salt-project-package-repo-migration-and-guidance/. 

Vagrant. Install Vagrant. URL: https://developer.hashicorp.com/vagrant/docs/installation. 






































  
