# Pkg-File-Service

## Summary

SSH server port changes can be automated with Salt using the pkg–file–service model. (Tero Karvinen 2018)


### Adding an SSH port manually

This task follows the instructions of (Tero Karvinen 2018).

I started the task by logging into the minion with the command vagrant ssh t002.
Next, I opened the SSH configuration with the command sudo nano /etc/ssh/sshd_config and added ports 22 and 1234 to the file.

<img width="643" height="670" alt="image" src="https://github.com/user-attachments/assets/5fb067db-a9d0-456f-bf40-50af8da434ad" />

After this, I restarted the SSH service with the command sudo systemctl restart ssh.

<img width="643" height="335" alt="image" src="https://github.com/user-attachments/assets/e79775a8-96a3-4148-a363-813132152442" />

I checked that SSH was listening on port 1234:

<img width="549" height="64" alt="image" src="https://github.com/user-attachments/assets/e67e2f6a-f236-416e-beeb-5857f4ad401f" />

### Breaking it manually

Next, I moved to the configuration file with the command sudo nano /etc/ssh/sshd_config and removed port 1234. After this, I restarted with the command sudo systemctl restart ssh.

I entered the command nc -vz localhost 1234.

<img width="643" height="51" alt="image" src="https://github.com/user-attachments/assets/51fadd17-8f72-4276-8529-ab9664283434" />

The result was Connection refused, meaning port 1234 was no longer listening.

### Salt state for the master

This task follows the instructions of (Aapo Tavio 2025).

I logged into the master with the command vagrant ssh t001.
I created a directory with the command sudo mkdir -p /srv/salt/sshdemon and moved into it with the command cd /srv/salt/sshdemon.

Next, I created a file with the command sudoedit ssh_dem_conf and added the following content to it:

<img width="280" height="68" alt="image" src="https://github.com/user-attachments/assets/fb04f0b0-0099-4689-89a5-9d4ed2042588" />

### File-Service state

I created the state file with the command sudoedit init.sls.
I added the following content to the file:

<img width="439" height="380" alt="image" src="https://github.com/user-attachments/assets/eac96de3-6389-468c-9701-13e3849ed634" />

Next, I ran the command sudo salt ’*’ state.apply sshdemon.

<img width="577" height="286" alt="image" src="https://github.com/user-attachments/assets/4c1755e2-6fc8-40eb-aaa5-9e8fa5495b37" />


<img width="421" height="146" alt="image" src="https://github.com/user-attachments/assets/70a0991f-1eee-4dd4-a303-1a2b799b43fc" />


<img width="351" height="349" alt="image" src="https://github.com/user-attachments/assets/999fe60f-c9ba-4a0c-b568-628002225286" />

I logged into the minion with the command vagrant ssh t002 and tested the connection with the command nc -vz localhost 1234.

<img width="561" height="43" alt="image" src="https://github.com/user-attachments/assets/57381dd8-f625-47aa-b351-e9e445239d77" />

Sources:

Karvinen, T. 3 April 2018. Pkg-File-Serice – Control Daemons with Sal - Change SSH Server Port. URL: https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh. 

Tavio, A. 2025. H4 Pkg-file-service. URL: https://aapotavio.com/configuration-management-systems/h4-pkg-file-service/. 















