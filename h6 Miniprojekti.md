# Web-palvelin – Nginx + HTML-sivu | Fanny Harju & Satu Harjula

Tämän projektin tarkoituksena on asentaa Nginx-webpalvelin ja julkaista oma HTML-sivu automaattisesti yhdellä Salt-tilalla.
Nginx on avoimen lähdekoodin ohjelmisto, jota käytetään pääasiassa verkkopalvelimena, mutta voidaan käyttää myös välityspalvelimena (reverse proxy), kuormantasaajana (load balancer) ja välimuistina (caching). (Nginx.org, 2025)

Aloitimme projektin tekemällä uuden virtuaalikoneen. Ajattelimme, että toinen ottaisi SSH-yhteyden toisen koneeseen ja tekisimme yhdessä projektia samalle koneelle. Oli kuitenkin SSH-yhteyden muodostamiesssa useita ongelmia, joten päätimme tehdä projektia omilla koneillamme.

Teimme projektin vanhalle virtuaalikoneelle, koska emme saaneet uutta toimimaan. Koneelle oli jo asenettuna Salt, mutta tarkistin sen vielä komennolla "Sudo salt-call --local test.ping" ja sain tulostuksena 'True'.

Loimme ensimmäiseksi rakenteen komennolla "sudo mkdir -p /srv/salt/web/files" ja siirryimme hakemistoon cd:llä.

Määritimme sitten mitä stateja ajetaan top.sls-tiedostossa komennolla "sudo nano /srv/salt/top.sls" ja kirjoitimme sinne seuraavan:

```yaml
base:

'*':

    - web

Tämän jälkeen avasimme init.sls-tiedoston komennolla "sudo nano /srv/salt/web/init.sls". Tiedostoon sisällytimme ohjeet Nginxin asentamiseen ja HTML-sivun paikoilleen laittamisen. (Salt Project, 2025) Kuvassa näkyy tiedoston sisältö:

<img width="608" height="230" alt="image" src="https://github.com/user-attachments/assets/247d9542-70c1-4a42-9888-0f19c6222f3b" />

Seuraavaksi kirjoitimme HTML-koodin, joka lopulta näkyy selaimessa. Teimme tämän index.html:ssä komennolla "sudo nano /srv/salt/web/files/index.html". Kuva alla.


<img width="568" height="223" alt="image" src="https://github.com/user-attachments/assets/93885720-3de3-43cd-b186-8beca8af41a9" />

Seuraavaksi ajoimme projektin komennolla sudo salt-call --local state.apply

<img width="639" height="590" alt="image" src="https://github.com/user-attachments/assets/335130c9-ba22-489f-9082-e2700995332b" />

Lopuksi tarkistimme, että teksti näkyy http://localhost verkkoselaimessa.


<img width="543" height="303" alt="image" src="https://github.com/user-attachments/assets/af8dd534-9686-4cbf-ba9c-4fa8553beb7c" />

Kaikki toimii, joten projekti sai päätöksen!



## Lähteet:

Nginx - https://nginx.org/

Salt Project, 2025. Salt.States.File. Luettavissa: https://docs.saltproject.io/en/latest/ref/states/all/salt.states.file

Salt Project, 2025. Salt.States.Pkg. Luettavissa: https://docs.saltproject.io/en/latest/ref/states/all/salt.states.pkg

Salt Project, 2025. The Top File. Luettavissa: https://docs.saltproject.io/en/3006/ref/states/top.html

Tero Karvinen, 2025. Palvelinten hallinta. Luettavissa: https://terokarvinen.com/palvelinten-hallinta/#laksyt















