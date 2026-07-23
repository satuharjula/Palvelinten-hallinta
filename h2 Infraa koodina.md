# h2 Infrastructure as Code


## Summary
### Hello Salt Infra-as-Code

- A custom state is created at /srv/salt/hello/init.sls, which ensures that the file /tmp/hello-example exists.
- The command sudo salt-call --local state.apply hello runs the state locally.
- After the local run, the resulting output describes in detail what was done. (Karvinen, 3.4.2024)

### Salt overview
- Salt uses YAML format to describe configurations and states.
- YAML is based on key-value pairs and uses spaces, not tabs.
- YAML has three basic elements, which are scalar, list, and dictionary.
- YAML's structure is determined by indentation. (Salt Project 2025)

### The Top File
- The top file determines which states are run on which machine.
- Its location is at the root of the state tree and it is named top.sls.
- A single top.sls file can be used to manage which states are installed and run on different machines simultaneously. (Salt Project 2025)


## Testing infrastructure code locally

This task follows the instructions of (Tero Karvinen 3.4.2024).

I started by fetching package updates with the command sudo apt-get update. After that, I installed the Micro editor with the command sudo apt-get -y install micro. Then I ran the command export EDITOR=micro, which sets Micro as the default editor. Next, I created a folder called hello at the path /srv/salt/ with the command sudo mkdir -p /srv/salt/hello, and moved into the folder with the command cd /srv/salt/hello.
<img width="559" height="97" alt="image" src="https://github.com/user-attachments/assets/01549349-bcea-4830-8781-e872af682a8e" />

Next, I ran the command sudoedit init.sls, which opened the Micro editor that I had just installed. I added the following content to the editor:

<img width="408" height="314" alt="image" src="https://github.com/user-attachments/assets/65cd75ec-87b9-48bc-a290-c5775b2f7c01" />

I ran the command sudo salt-call --local state.apply hello, which printed a summary as shown in the image:

<img width="637" height="369" alt="image" src="https://github.com/user-attachments/assets/c881354f-0780-474e-b717-2ce62e2c5b22" />

The output indicated that the file /tmp/hellosatu had been created successfully, since it stated "file /tmp/hellosatu created." I also verified with the command ls /tmp/hellosatu that the file actually existed. When the same command is run again, "changed (1)" disappears, since nothing needs to be changed anymore. This shows that Salt is working correctly and that the state is idempotent.

<img width="547" height="39" alt="image" src="https://github.com/user-attachments/assets/8c050f5e-aa57-41b9-ae31-908b29dff572" />
<img width="547" height="39" alt="image" src="https://github.com/user-attachments/assets/9aabf67f-8d4b-4837-a263-0953e7e1612f" />

I then went back to the hellosatu file and added the content "Hei maailma!" ("Hello world!").
<img width="616" height="357" alt="image" src="https://github.com/user-attachments/assets/03b1c48d-da57-47e2-a3a3-4b420df5aa6e" />
<img width="624" height="55" alt="image" src="https://github.com/user-attachments/assets/31c89533-ec4b-43d1-b8bc-cbbb1918041d" />

I checked with the command cat /tmp/hellosatu that the file existed and showed the desired content.


## Top file: running all states with a single command

I started by running the command sudoedit /srv/salt/top.sls, which opened the editor, and I added the following sections there:
<img width="584" height="315" alt="image" src="https://github.com/user-attachments/assets/56c3ac45-34a5-411b-a0b2-13c622549754" /> (Salt project 2025)

After this, I saved and closed the editor. I first tested running a single state by executing sudo salt-call --local state.apply hello, which worked.
<img width="632" height="309" alt="image" src="https://github.com/user-attachments/assets/5de65ecf-1ee7-4f6b-817a-5cacec375e35" />

Next, I ran all the states listed in the top file with the command sudo salt-call --local state.apply, and the output confirmed that the state was correct ("File /tmp/hellosatu is in the correct state").

<img width="627" height="298" alt="image" src="https://github.com/user-attachments/assets/bf5c8c64-cefa-4a76-b0b4-815e3dff75dd" />


## Five example state functions

I started by creating folders for each of the five state functions with the command sudo mkdir -p /srv/salt/{hellopkg,hellofile,helloservice,hellouser,hellocmd}.

### pkg state function:

I moved into the hellopkg directory with the command cd /srv/salt/hellopkg, after which I ran the command sudoedit init.sls, which moved me into the editor.
<img width="491" height="208" alt="image" src="https://github.com/user-attachments/assets/576d5e78-623a-49cb-adcf-c2d123da68ec" /> (Salt project 2025)

Next, I ran the command sudo salt-call --local state.apply hellopkg.
<img width="635" height="326" alt="image" src="https://github.com/user-attachments/assets/be810d9d-2b47-427d-b04c-d15e98710153" />
Salt checked whether htop was already installed. It was not, so it installed it.

### file state function:

I moved into the hellofile directory with the command cd /srv/salt/hellofile, after which I ran the command sudoedit init.sls to access the editor.
<img width="602" height="165" alt="image" src="https://github.com/user-attachments/assets/4d28eaa3-75b1-4fdb-a0e8-0553ae1ef95a" />

Next, I ran the command sudo salt-call --local state.apply hellofile
<img width="636" height="336" alt="image" src="https://github.com/user-attachments/assets/4153401c-b4c6-41ed-9970-b45626491923" /> (Salt project 2025)

I added more content to the file, meaning I went back into the editor with the command sudoedit init.sls.

<img width="315" height="158" alt="image" src="https://github.com/user-attachments/assets/f1eb4172-1122-4d58-a4e7-ab0194225376" />

I ran the command sudo salt-call --local state.apply hellofile again.

<img width="638" height="352" alt="image" src="https://github.com/user-attachments/assets/c857ea60-25e0-4fe0-8e52-5af94c35dee0" />

The output confirmed success with the line "File /tmp/hello.file.txt updated," meaning Salt detected the change and implemented it.

### service state function:

I moved into the helloservice directory with the command cd /srv/salt/helloservice and into the editor with the command sudoedit init.sls.

<img width="563" height="133" alt="image" src="https://github.com/user-attachments/assets/61027f4f-d95b-4d06-9f87-1f7db3a6478c" /> (Salt project 2025)

After this, I installed the OpenSSH server with the commands sudo apt update and sudo apt install -y openssh-server.
Next, I ran the command sudo salt-call --local state.apply helloservice.

<img width="449" height="238" alt="image" src="https://github.com/user-attachments/assets/339b7e27-3cc2-4de7-96c1-20c8ecdc9d23" />

The output showed that the service was already enabled, so Salt made no changes.

### user state function:

I moved into the directory with the command cd /srv/salt/hellouser, after which into the editor with the command sudoedit init.sls.

<img width="289" height="167" alt="image" src="https://github.com/user-attachments/assets/ecadfc7a-bbdc-41ee-a25c-2f07ff612888" /> (Salt project 2025)

Next, I ran the command sudo salt-call --local state.apply hellouser.

<img width="485" height="403" alt="image" src="https://github.com/user-attachments/assets/b234bc4e-a8ff-4a9d-ab7e-cd7d0dd40d58" />

The output showed that the user was created with UID and GID 1001, with home directory /home/testi and shell /bin/sh.

### cmd state function

I moved into the directory with the command cd /srv/salt/hellocmd, after which into the editor with the command sudoedit init.sls.

<img width="413" height="159" alt="image" src="https://github.com/user-attachments/assets/c22f9c1c-751e-47de-b1c5-9213a75676d5" /> (Salt project 2025)

Next, I ran the command sudo salt-call --local state.apply hellocmd.

<img width="634" height="381" alt="image" src="https://github.com/user-attachments/assets/70eeb64b-2eec-407d-bb05-e463c2a7acb5" />

The state's command 'Heii' was run and the file was created.

I then checked the content with the command cat /tmp/once.txt.

<img width="446" height="64" alt="image" src="https://github.com/user-attachments/assets/6ee16f0d-0f8a-4961-ae50-e4fbe2527d49" />


## SLS with two state functions

I started by creating a new folder with the command sudo mkdir -p /srv/salt/apache and moved into this folder with the command cd /srv/salt/apache. Next, I moved into the editor with the command sudoedit init.sls.

<img width="302" height="197" alt="image" src="https://github.com/user-attachments/assets/9d2d4c4c-3b2c-4b29-860b-3a66a447c8bc" /> (Salt project 2025)

I ran the command sudo salt-call --local state.apply apache. 

<img width="626" height="521" alt="image" src="https://github.com/user-attachments/assets/9441b2ee-cc6e-4e49-9a5c-e512d3494182" />
<img width="634" height="796" alt="image" src="https://github.com/user-attachments/assets/aca7201b-d8e7-4e5e-a480-5acf49eebbee" />

I also tested running the command sudo salt-call --local state.apply apache multiple times to verify that my SLS file was idempotent.

<img width="634" height="403" alt="image" src="https://github.com/user-attachments/assets/297b4e96-ac4c-48df-9ccd-ba744fecb563" />

I also tested that Apache was running and would start automatically. I used the command systemctl is-active apache2 && systemctl is-enabled apache2. With the command curl -I http://localhost/ | head -n1 I tested that Apache responds to HTTP requests. (Red Hat Documentation 2025)

<img width="614" height="63" alt="image" src="https://github.com/user-attachments/assets/d58c004d-a5f5-4a38-b8b2-f942920c1a83" />

## Sources:

Red Hat Documentation 2025 . Chapter 11. Managing systemd. URL: https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/8/html/configuring_basic_system_settings/managing-systemd_configuring-basic-system-settings. 

Salt project 2025. How do I use salt states. URL: https://docs.saltproject.io/en/3006/topics/tutorials/starting_states.html.

Salt Project 2025. Salt overview. URL: https://docs.saltproject.io/salt/user-guide/en/latest/topics/overview.html#rules-of-yaml.

Salt project 2025. Salt.states.cmd. URL: https://docs.saltproject.io/en/3007/ref/states/all/salt.states.cmd.html.

Salt project 2025. Salt.states.file. URL: https://docs.saltproject.io/en/3006/ref/states/all/salt.states.file.html.

Salt project 2025. Salt.states.pkg. URL: https://docs.saltproject.io/en/latest/ref/states/all/salt.states.pkg.html.

Salt project 2025. Salt.states.service. URL: https://docs.saltproject.io/en/3007/ref/states/all/salt.states.service.html.

Salt project 2025. Salt.states.user. URL: https://docs.saltproject.io/en/3007/ref/states/all/salt.states.user.html.

Karvinen, T. 3 April 2024. Hello Salt Infra-as-Code. URL: https://terokarvinen.com/2024/hello-salt-infra-as-code/. 


