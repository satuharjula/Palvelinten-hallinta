# Pkg-File-Service

## Tiivistelmä



### SSH-portin lisääminen käsin

Tehtävässä mukailtu (Tero Karvinen 2018) ohjeita.

Aloitin tehtävän kirjautumalla minionille komennolla vagrant ssh t002.
Seuraavaksi avasin SSH-konfiguraation komennolla sudo nano /etc/ssh/sshd_config ja lisäsin tiedostoon portit 22 ja 1234.

<img width="643" height="670" alt="image" src="https://github.com/user-attachments/assets/5fb067db-a9d0-456f-bf40-50af8da434ad" />

Tämän jälkeen käynnistin ssh-palvelun uudelleen komennolla sudo systemctl restart ssh.

<img width="643" height="335" alt="image" src="https://github.com/user-attachments/assets/e79775a8-96a3-4148-a363-813132152442" />

Tarkistin, että SSH kuuntelee portissa 1234:

<img width="549" height="64" alt="image" src="https://github.com/user-attachments/assets/e67e2f6a-f236-416e-beeb-5857f4ad401f" />

### Rikkominen käsin

Seuraavaksi siirryin configurointitiedostoon komennolla sudo nano /etc/ssh/sshd_config ja poistin portin 1234. Tämän jälkeen käynnistin uudelleen komennolla sudo systemctl restart ssh.

Syötin komennon nc -vz localhost 1234.

<img width="643" height="51" alt="image" src="https://github.com/user-attachments/assets/51fadd17-8f72-4276-8529-ab9664283434" />

Lopputulema oli Connection refused, eli portti 1234 ei enää kuuntele. 

### Salt-tila masterille

Tehtävässä mukailtu (Aapo Tavio 2025) ohjeita.

Kirjauduin masterille komennolla vagrant ssh t001.
Loin hakemiston komennolla sudo mkdir -p /srv/salt/sshdemon ja siirryin siihen komennolla cd /srv/salt/sshdemon.

Seuraavaksi loin tiedoston komennolla sudoedit ssh_dem_conf ja lisäsin sinne sisällön:

<img width="280" height="68" alt="image" src="https://github.com/user-attachments/assets/fb04f0b0-0099-4689-89a5-9d4ed2042588" />

### File-Service-tila

Loin tilatiedoston komennolla sudoedit init.sls.
Lisäsin tiedostoon sisällön:

<img width="439" height="380" alt="image" src="https://github.com/user-attachments/assets/eac96de3-6389-468c-9701-13e3849ed634" />

Seuraavaksi ajoin komennon sudo salt ’*’ state.apply sshdemon.

<img width="577" height="286" alt="image" src="https://github.com/user-attachments/assets/4c1755e2-6fc8-40eb-aaa5-9e8fa5495b37" />

<img width="421" height="146" alt="image" src="https://github.com/user-attachments/assets/70a0991f-1eee-4dd4-a303-1a2b799b43fc" />

<img width="351" height="349" alt="image" src="https://github.com/user-attachments/assets/999fe60f-c9ba-4a0c-b568-628002225286" />

Kirjauduin minionille komennolla vagrant ssh t002 ja testasin yhteyttä komennolla nc -vz localhost 1234.

<img width="561" height="43" alt="image" src="https://github.com/user-attachments/assets/57381dd8-f625-47aa-b351-e9e445239d77" />

Lähteet:
Karvinen, T. 3.4.2018. Pkg-File-Serice – Control Daemons with Sal - Change SSH Server Port. Luettavissa: https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh.

Tavio, A. 2025. H4 Pkg-file-service. Luettavissa: https://aapotavio.com/configuration-management-systems/h4-pkg-file-service/. 















