# Web Server – Nginx + HTML Page | Fanny Harju & Satu Harjula

The purpose of this project is to install an Nginx web server and publish our own HTML page automatically using a single Salt state.
Nginx is open-source software mainly used as a web server, but it can also be used as a reverse proxy, load balancer, and cache. (Nginx.org, 2025)

We started the project by creating a new virtual machine. We thought one of us would establish an SSH connection to the other's machine and we would work on the project together on the same machine. However, there were several problems establishing the SSH connection, so we decided to do the project on our own machines.

We did the project on the old virtual machine, since we couldn't get the new one working. Salt was already installed on the machine, but I still checked it with the command "Sudo salt-call --local test.ping" and got 'True' as the output.

First, we created the structure with the command "sudo mkdir -p /srv/salt/web/files" and moved into the directory with cd.

We then defined which states would be run in the top.sls file with the command "sudo nano /srv/salt/top.sls" and wrote the following there:

```yaml
base:

'*':

    - web
``` 

After this, we opened the init.sls file with the command "sudo nano /srv/salt/web/init.sls". In the file, we included instructions for installing Nginx and putting the HTML page in place. (Salt Project, 2025) The image shows the content of the file:

<img width="608" height="230" alt="image" src="https://github.com/user-attachments/assets/247d9542-70c1-4a42-9888-0f19c6222f3b" />

Next, we wrote the HTML code that would ultimately be displayed in the browser. We did this in index.html with the command sudo nano /srv/salt/web/files/index.html. Image below.


<img width="568" height="223" alt="image" src="https://github.com/user-attachments/assets/93885720-3de3-43cd-b186-8beca8af41a9" />

Next, we ran the project with the command sudo salt-call --local state.apply

<img width="639" height="590" alt="image" src="https://github.com/user-attachments/assets/335130c9-ba22-489f-9082-e2700995332b" />

Finally, we checked that the text appeared at http://localhost in the web browser.


<img width="543" height="303" alt="image" src="https://github.com/user-attachments/assets/af8dd534-9686-4cbf-ba9c-4fa8553beb7c" />

The HTML page loaded, so the project was completed!



## Sources:

Nginx. URL: https://nginx.org/

Salt Project, 2025. Salt.States.File. URL: https://docs.saltproject.io/en/latest/ref/states/all/salt.states.file

Salt Project, 2025. Salt.States.Pkg. URL: https://docs.saltproject.io/en/latest/ref/states/all/salt.states.pkg

Salt Project, 2025. The Top File. URL: https://docs.saltproject.io/en/3006/ref/states/top.html

Tero Karvinen, 2025. Palvelinten hallinta. URL: https://terokarvinen.com/palvelinten-hallinta/#laksyt















