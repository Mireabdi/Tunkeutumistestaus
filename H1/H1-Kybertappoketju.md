# Tunkeutumistestaus

### Abdirahman Mire
## ICI005AS3A-3005

### H1 Kybertappoketju

### X) Artikkelit

Darknet Diaries jakso 113: Adam

- Adam saa työpaikan koulun IT-tehtävissä ja huomasi että local admin password toimi kaikkiin koneisiin.

- Irtisanotaan tehtävästä taustatutkimuksen takia.

- Usean vuoden kulutta opittuaan lisää it taitoja, muistaa saman haavoittuvaisuuden koulun järjestelmäassä.

- Kirjautuu koulun järjestelmään ja hankki luvattomasti pääkäyttäjänoikeudet (Privilege escalation).
   
- Tunnuksilla luki toisten sähköposteja ja viestejä. Muokkasi opettajien ja ylläpitäjien käyttäjätilejä.

- Luvaton toiminta havaittiin jäjestelmän lokitiedoista joka johti pidätykseen.

  

Abstract, 3.2 Intrusion Kill Chain.

- Intrusion Kill Chain malli jakaa kyberhyökkäykset seitsemään eri vaiheeseen: tiedustelu, aseistaminen, toimitus, hyväksikäyttö, asennus, komentokanava ja tavoitteiden saavuttaminen.

- Auttaa puolustajia ymmärtämään hyökkäyksen kulun ja keskeyttämään sen mahdollisimman aikaisessa vaiheessa.

Surveying Essential Tools for Active Reconnaissance. 

- Active reconnaissance: tiedostelua, esim porttiskannausta haavoittuvaisuuksien löytämiseksi.

- Nmap: monipuolisin ja vakain porttiskanneri.



KKO 003:36

- 17-vuotias yritti murtautua Osuuspankin tietojärjestelmään porttiskannauksen avulla.

- Todettiin että porttiskannaus oli rikos ja tuomittiin maksamaan vahingonkorvausta noin 12 600e 



### A) Kali linuxin Versio: 2025.3 asennus

Sujui ongelmitta, Latasin ensin VMwaren jonka jälkeen VMware version Kali Linuxista.

![kuva1](/H1/kuvat/kuva1.png)

### B) irrota Kali-virtuaalikone verkosta:

![kuva1](/H1/kuvat/kuva2.png)

offline tilassa pingasin 8.8.8.8
### C) Porttiskannaus: `nmap -T4 -A localhost`. 

Parametrit sain selvitettyä komennolla `man nmap` ja etsin komennolla `/-A` 
#### Parametrit:
`-T4`: Nopea skannaus. `-A`: tunnistaa OS ja version

![kuva1](/H1/kuvat/kuva4.png)
![kuva1](/H1/kuvat/kuva3.png)

Skannasin offline-tilassa:  `nmap -T4 -A localhost`. Kaikki 1000 porttia ovat kiinni

(unohdin ottaa screenshotin tästä kohtaa, pahoittelut.)

### D) Demonien asennus ja uudelleen skannaus: 
Latasin demonit: Apache2 (HTTP-palvelin) ja vsftpd (FTP-palvelin) 

komennot:

Apache2 

`sudo apt update`
`sudo apt install apache2 -y`
`sudo systemctl start apache2`
`sudo systemctl enable apache2` 

vsftpd 

`sudo apt install vsftpd -y`
`sudo systemctl start vsftpd`
`sudo systemctl enable vsftpd`

uudelleen skannaus:

![kuva1](/H1/kuvat/kuva5.png)

Skannasin offline-tilassa. Erona edelliseen, nyt näyttää olevan kaksi porttia(21 ftp ja 80 http) auki 

### E ja F) Metasploitable 2.

Latasin ja purkasin Metasploitable 2 jonka jälkeen lisäsin sen VMwareen. Eristääkseni verkon muokkasin verkkoadapterin asetuksia niin että KaliVM:llä on kaksi adapteria (NAT ja Host) ja Metasploitablella on vain yksi adapteri (Host-only). 

Seuraavaski tarkistin metasploitable 2 IP-osoitteen komennolla `ifconfig`  ja pingasin sitä KaliVM-koneesta.

![kuva1](/H1/kuvat/kuva6.png)

### G)Etsi Metasploitable porttiskannaamalla `nmap -sn`

![kuva1](/H1/kuvat/kuva7.png)

offline tilassa käytin `nmap -sn` joka antoi vastauksen No targets were specified ja ymmärsin että pitää laittaa IP osoite perään. 

![kuva1](/H1/kuvat/Kuva8.png)

### H) Metasploitable porttiskannaus komennolla `nmap -A -T4 -p-` 

Hyökkääjälle kiinnostavat portit:

Portti 23 Telnet

![kuva1](/H1/kuvat/kuva9.png)

Haavoittuvaisuus 1: Telnet näyttää salasanat selvässä tekstissä ilman mitään salausta.

Portti 21 FTP

![kuva1](/H1/kuvat/kuva10.png)

Haavoittuvaisuus 2: Anonymous FTP login allowed. Antaa luvan anonyyminä ladata ja lukea tiedostoja.


#### Referenssit: 

Karvinen: https://terokarvinen.com/tunkeutumistestaus/

IBM: https://www.ibm.com/docs/en/i/7.5.0?topic=i-configuring-anonymous-ftp

lockhead Martin: https://lockheedmartin.com/content/dam/lockheed-martin/rms/documents/cyber/LM-White-Paper-Intel-Driven-Defense.pdf

KKO2003:36 :https://finlex.fi/fi/oikeuskaytanto/korkein-oikeus/ennakkopaatokset/2003/36

Darknet diaries 113: Adam  :https://darknetdiaries.com/episode/113/

https://www.oreilly.com/videos/the-art-of/9780135767849/9780135767849-SPTT_04_00/

