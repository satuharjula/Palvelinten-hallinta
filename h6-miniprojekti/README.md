# Web Server – Nginx + HTML Page | Fanny Harju & Satu Harjula  

The purpose of this project is to install an Nginx web server and automatically publish a custom HTML page using Salt, all with a single command.  

## How the Project Works  

In this project, a single Salt state does everything needed:  

- Installs the Nginx server (`pkg.installed`)  
- Starts the service (`service.running`)  
- Copies a custom `index.html` page (`file.managed`) to the `/var/www/html/index.html`          directory  
- The result is visible in the browser at `http://localhost`  

## Result  

<img width="543" height="303" alt="image" src="https://github.com/user-attachments/assets/af8dd534-9686-4cbf-ba9c-4fa8553beb7c" />  

## License  

This project is licensed under the GPLv3 license. See the LICENSE file for more details.  
