# Web-palvelin – Nginx + HTML-sivu | Fanny Harju & Satu Harjula

Tämän projektin tarkoituksena on asentaa Nginx-webpalvelin ja julkaista oma HTML-sivu automaattisesti Saltin avulla yhdellä komennolla.

## Projektin toiminta

Projektissa yksi Salt state tekee kaiken tarvittavan:

- Asentaa Nginx-palvelimen (`pkg.installed`)
- Käynnistää palvelun (`service.running`)
- Kopioi oman `index.html`-sivun (`file.managed`) hakemistoon `/var/www/html/index.html`
- Lopputulos näkyy selaimessa osoitteessa `http://localhost`

## Lopputulos 

<img width="543" height="303" alt="image" src="https://github.com/user-attachments/assets/af8dd534-9686-4cbf-ba9c-4fa8553beb7c" />

## Lisenssi

Projekti on lisensoitu GPLv3-lisenssillä. Katso tarkemmat tiedot tiedostosta LISENSSI.
