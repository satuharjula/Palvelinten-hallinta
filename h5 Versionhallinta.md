# h5 Versionhallinta

## Tiivistelmä
### Chacon and Straub 2014: 

- Git on versionhallintajärjestelmä, jonka avulla hallitaan projektien muutoksia.
- Toimii paikallisesti, eli commitit ja historia ovat aina omalla koneella.

### git add . && git commit; git pull && git push

- git add . -komennon tehtävänä on lisätä tiedoston sisältö indeksiin. (Git)
- && -komennossa suoritta seuraavan komennon vain jos edellinen onnistui. (GeeksforGeeks 2020)
- git commit -komennon tehtävänä on tallentaa muutokset arkistoon. (Git)
- ; on komentojen erotin. (GeeksforGeeks 2020)
- git pull -komennon tehtävänä on hakea uudet commitit ja yhdistää ne nykyiseen haaraan. (Git)
- git push -komennon tehtävänä on lähettää paikallisesti tehdyt commitit etärepositorioon. (GitHub Docs 2025)

  ### Commits

  - Repo kehitys: Perusrakenteen luonti, hello world Salt-moduuli ja lopuksi pienten parannuksien lisäys. (Tero Karvinen 2024)

## Online

Tein Githubiin uuden repositoryn nimeltä snow-project. 

<img width="634" height="254" alt="image" src="https://github.com/user-attachments/assets/6a0f5f7e-e325-4ce2-a500-c2f4069697a6" />


## Dolly

Loin uuden SSH-avaimen komennolla ssh-keygen. Tarkistin ja kopioin julkisen avaimen komennolla cat ~/.ssh/id*.pub, jonka jälkeen lisäsin sen GitHubiin.
Testasin yhteyden Githubiin komennolla ssh -T git@github.com.

<img width="632" height="26" alt="image" src="https://github.com/user-attachments/assets/4f453484-ec3f-4710-acc3-e3e43f1969b8" />

Seuraavaksi loin kansion nimeltä project komennolla mkdir project ja siirryin cd ~/project -komennolla siihen. Ajoin komennon git clone git@github.com:satuharjula/snow-project.git snow-project-ssh. 

<img width="618" height="101" alt="image" src="https://github.com/user-attachments/assets/e253c27c-ff0b-4e92-8cd5-fdf3bba151ef" />

Siirryin cd snow-project-ssh ja syötin komennon git remote -v, jotta näin, että repo on kloonattu.

<img width="614" height="36" alt="image" src="https://github.com/user-attachments/assets/34273cac-adfe-4f73-bdb1-9c740ee7b1a5" />

Seuraavaksi siirryin SSH-kloonattuun kansioon komennolla cd ~/project/snow-project-ssh ja avasin README.md:n komennolla nano README.md.

Lisäsin README.md -tiedostoon sisältöä:

<img width="631" height="101" alt="image" src="https://github.com/user-attachments/assets/69059602-5a4b-48ef-b3bc-2fa736f97309" />

Tarkistin muutoksen komennolla git status.

<img width="635" height="148" alt="image" src="https://github.com/user-attachments/assets/f7c9bd60-2090-4e3b-8df0-b744b20e6835" />

Tein commitin komennoilla git add README.md ja git commit -m ”Test change”.

<img width="628" height="31" alt="image" src="https://github.com/user-attachments/assets/19daa1ca-a215-44da-9896-bc0f9a0727b1" />

Pushasin muutoksen Gittiin komennolla git push origin main.

<img width="624" height="122" alt="image" src="https://github.com/user-attachments/assets/80eed779-68d7-4d35-9898-b4076081d70e" />

Lopuksi tarkistin, että muutos näkyi GitHubissa. (Git)

<img width="506" height="394" alt="image" src="https://github.com/user-attachments/assets/d2aeb17c-e9e7-40b2-aa27-7645b64eda31" />


## Doh!

Siirryin muokkaamaan README.md tiedostoa komennolla nano README.md ja lisäsin sotkua.

<img width="602" height="116" alt="image" src="https://github.com/user-attachments/assets/f97c8ef5-34e4-417f-8c83-eaa24f09e6ee" />

Syötin komennon git status tarkistaakseni, että git huomaa muutoksen.

<img width="632" height="147" alt="image" src="https://github.com/user-attachments/assets/52abedd6-ca9b-40a7-8c24-4af4d627961b" />

Seuraavaksi syötin komennon git reset --hard, jolloin git palauttaa tiedostot viimeisimmän commitin mukaiseen tilaan.

Tämän jälkeen syötin komennon git status, jotta nään, että muutos katosi.

<img width="632" height="107" alt="image" src="https://github.com/user-attachments/assets/6fd85aa5-7c5d-48ad-b4c1-b68a836873d5" />

Lopuksi vielä tarkistin cat README.md -komennolla, että tekstini oli kadonnut. 

<img width="603" height="76" alt="image" src="https://github.com/user-attachments/assets/6ea6ca5a-9fcf-4bcd-81bd-a808c211cdc9" />

## Log

Tarkastelin lokiani komennolla git log. Komento näyttää tekijän nimen sekä sähköpostiosoitteen, ajankohdan, jolloin commit on tehty ja viestin, joka kertoo lyhyesti, mitä on muutettu.

<img width="991" height="221" alt="image" src="https://github.com/user-attachments/assets/51f400d3-33b8-4615-970d-b29c110e3dcf" />

## Salted shard

Siirryin repoon komennolla cd ~/project/snow-project ja tein uuden salt-hakemiston komennolla mkdir -p salt ja loin hakemiston sisälle top.sls tiedoston komennolla nano salt/top.sls.

Lisäsin top.sls sisällön:

<img width="532" height="187" alt="image" src="https://github.com/user-attachments/assets/2671a145-9cd4-4896-8fb9-2235175d004a" />

Loin salt-hakemiston sisälle test.sls-tiedoston komennolla nano salt/test.sls.

Lisäsin test.sls sisällön:

<img width="577" height="137" alt="image" src="https://github.com/user-attachments/assets/2b431b16-c178-4937-90ac-05deb3319e7a" />

Ajoin Salt-tilat komennolla sudo salt-call --local --file-root salt/ state.apply.

<img width="623" height="266" alt="image" src="https://github.com/user-attachments/assets/e05f2f76-2a8b-489f-a97e-1291c45d07d3" />

Lopuksi lisäsin Salt-tiedostot versionhallintaan ja lähetin ne Githubiin seuraavilla komennoilla:

<img width="643" height="223" alt="image" src="https://github.com/user-attachments/assets/20721460-3ddf-4921-a25b-f72c334a0be6" />

Tarkistin, että tiedostot näkyvät GitHubin snow-project:ssa:

<img width="418" height="283" alt="image" src="https://github.com/user-attachments/assets/0d64006d-3172-4126-b1da-9ff48b7b840f" />

<img width="443" height="271" alt="image" src="https://github.com/user-attachments/assets/96c15b8c-9000-4094-a72b-ffbf21335cf6" />


## Lähteet:

GeeksforGeeks. 14.10.2020. Difference Between && and ; chaining operators in Linux. Luettavissa: https://www.geeksforgeeks.org/linux-unix/difference-between-chaining-operators-in-linux/. Luettu: 23.11.2025.

GitHub Docs. 2025. Pushing commits to a remote repository. Luettavissa: https://docs.github.com/en/get-started/using-git/pushing-commits-to-a-remote-repository. Luettu: 23.11.2025

Git. Luettavissa: https://git-scm.com/docs/git-add. Luettu: 23.11.2025.

GitHub. Karvinen, T. 10.4.2024. Suolax. Commits. Luettavissa: https://github.com/terokarvinen/suolax/commits/main/. Luettu: 23.11.2025. 
