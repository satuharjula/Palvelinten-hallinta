# h1 - The five  


## Summary  
### Install Salt on Debian 13 Trixie:  

Installing Salt on Debian 13 requires an APT package repository, through which Salt's packages can be fetched and verified. The repository includes a PGP key used to verify the packages' signatures, as well as a sources.list file where the public key is located. (Karvinen 20.10.2025)  

###	Run Salt Command Locally  

Salt is used to manage multiple slave machines. Salt commands are run locally, allowing the result to be seen immediately. The most important state functions are file, service, pkg, cmd, and user. (Karvinen 28.10.2021)  

###	Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux  

Slave machines can be managed even from behind a firewall or NAT, or from an unknown address. The master machine, which manages the slave machines, needs to have a public server and address. Each slave machine is assigned a different ID so that each one can be identified individually. Finally, the slave's key is accepted on the master machine. (Karvinen 28.3.2018)  

###	Writing the report  

•	Reproducibility  

    Anyone should be able to repeat the work in the same environment and achieve the same      result.  

•	Precision  

	The work steps should be described in detail, which command was used and when.  
	Successes and failures should be documented.  
	The report should be written in the past tense.  

•	Readability  

    Use of subheadings  
    Clear language  
    A summary at the beginning of the report, if desired  

•	Source references  

•	Plagiarism, fabrication, and unauthorized copying of images are strictly forbidden. (Karvinen 4.6.2006)  

## Installing Salt on Debian 13  
This task was based on the instructions by Karvinen (2025).  

### Downloading the PGP Public Key and the Salt Sources File  
I started the task by installing wget, so that I could download the necessary files.  

I installed wget with the commands sudo apt-get update and sudo apt-get install wget.  

After that, I created a new folder with the command mkdir saltrepo/ and moved into it with cd saltrepo/.  

Next, I downloaded the PGP public key with the command:  

wget https://packages.broadcom.com/artifactory/api/security/keypair/SaltProjectKey/public 

And the salt.sources file with the command:  

wget https://github.com/saltstack/salt-install-guide/releases/latest/download/salt.sources. (SALT PROJECT 2025)  

### Copying the Public Key and the salt.sources File  
Next, I copied the public key with the command: sudo cp public /etc/apt/keyrings/salt-archive-keyring.pgp  

and the salt.sources file with the command:  sudo cp salt.sources /etc/apt/sources.list.d/.  

This was done so that Salt's packages could be fetched and verified automatically.  

### Installing Salt  
After that, I updated with the command:  

sudo apt-get update

and installed Salt with the command:  

sudo apt-get install salt-minion salt-master. 

Next, I checked with the command sudo salt-call --version that the installation was successful.  

<img width="608" height="73" alt="image" src="https://github.com/user-attachments/assets/7ec99b4f-dc8e-4a28-a55c-276724584c5d" />

## The Five Most Important Salt State Functions  

### The pkg State Function  

I ran the command sudo salt-call –local -l info state.single pkg.installed tree. (Karvinen 28.10.2021)The result showed True, and the Changes section showed that the tree package was installed. Succeeded showed 1 (changed=1), meaning the operation was successful.
<img width="541" height="277" alt="image" src="https://github.com/user-attachments/assets/54ee41e7-fc1d-40c9-8912-8ee8adc2af98" />

### The file State Function  

I ran the command sudo salt-call - -local state.single file.managed /tmp/kokeilu, which ensured that the file exists. (Karvinen 28.10.2021) The result showed True, and the Changes section showed that the file /tmp/kokeilu was created. Succeeded showed 1 (changed=1), meaning the operation made a change and was successful.  

<img width="544" height="377" alt="image" src="https://github.com/user-attachments/assets/47bb9ea0-4836-4b05-acf2-bc269f51f71d" />

### The service State Function  

I ran the command sudo salt-call --local -l info state.single service.running apache2 enable=True. (Karvinen 28.10.2021) The output showed Result: False and ”The named sarvice apache2 is not available”. The command did not work because apache2 is not installed on my virtual machine.  
<img width="609" height="228" alt="image" src="https://github.com/user-attachments/assets/756818b0-533c-46af-96f9-ff11f6afb642" />

### The user State Function  

I ran the command sudo salt-call --local -l info state.single user.present satu. (Karvinen 28.10.2021) The result read ”User satu is present and up to date”,meaning the user already existed, so Salt did not make any changes, and the Changes section was therefore empty.   
<img width="547" height="188" alt="image" src="https://github.com/user-attachments/assets/b43e9c2a-2cd8-4843-b9b5-d51a10fbbd84" />

### The cmd State Function  

I ran the command sudo salt-call --local -l info state.single cmd.run 'touch /tmp/test' creates="/tmp/test". (Karvinen 28.10.2021) The result “Result: True” indicated that the run was successful. “Changes” showed that the command was executed and the file /tmp/test was created.  
<img width="529" height="264" alt="image" src="https://github.com/user-attachments/assets/cadbe002-c69c-4094-aada-f12b389e56ce" />  

## Idempotent  

I ran sudo salt-call --local -l info state.single user.present satu twice. (Karvinen 2021) The first run verified the user, and on the second run Salt reported “User satu is present and up to date” with Changes empty. This demonstrates idempotency — meaning the same state does not make an unnecessary change once it is already correct.

<img width="547" height="188" alt="image" src="https://github.com/user-attachments/assets/2bcd15bb-d51a-473f-ad41-7627eac733be" />

## Sources

Karvinen, T. 22 January 2021. Install Debian on Virtualbox – Updated 2024. URL: https://terokarvinen.com/2021/install-debian-on-virtualbox/. Accessed: 27 October 2025. 

Karvinen, T. 20 October 2025. Install Salt on Debian 13 Trixie. URL: https://terokarvinen.com/install-salt-on-debian-13-trixie/. Accessed: 26 October 2025. 

Karvinen, T. 28 October 2021. Run Salt Command Locally. URL: https://terokarvinen.com/2021/salt-run-command-locally/. Accessed: 26 October 2025.

Karvinen, T. 28 March 2018. Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux. URL: https://terokarvinen.com/2018/03/28/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/. Accessed: 26 October 2025. 

SALT PROJECT 2025. Linux (DEB). URL: https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/linux-deb.html. Accessed: 24 October 2025.




















