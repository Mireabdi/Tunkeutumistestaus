# Tunkeutumistestaus

## ICI005AS3A-3005
### H1 Kybertappoketju

### X) Artikkelit

### A) Kali linuxin Versio: 2025.3 asennus: Sujui ongelmitta, Latasin ensin VMwaren jonka jälkeen VMware version Kali Linuxista.

![kuva1](/H1/kuvat/kuva1.png)

### B) irrota Kali-virtuaalikone verkosta:

![kuva1](/H1/kuvat/kuva2.png)

### C) Porttiskannaus: `nmap -T4 -A localhost`. Parametrit sain selvitettyä komennolla `man nmap` ja etsin komennolla `/-A` 
#### Parametrit:
`-T4`: Nopea skannaus. `-A`: tunnistaa OS ja version

![kuva1](/H1/kuvat/kuva4.png)
![kuva1](/H1/kuvat/kuva3.png)

sammutin netin ja skannasin. Kaikki 1000 porttia ovat kiinni

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

Sammutin netin ja skannasin. Erona edelliseen, nyt näyttää olevan kaksi porttia(21 ftp ja 80 http) auki 

### E ja F) Metasploitable 2.

latasin ja purkasin Metasploitable 2 jonka jälkeen lisäsin sen VMwareen. Eristääkseni verkon muokkasin verkkoadapterin asetuksia niin että KaliVM:llä on kaksi adapteria (NAT ja Host) ja Metaspoiltablella on vain yksi adapteri (Host-only). 

Seuraavaski tarkistin metasploitable 2 IP-osoitteen komennolla `ifconfig`  ja pingasin sitä KaliVM-koneesta.

![kuva1](/H1/kuvat/kuva6.png)

### G)Etsi Metasploitable porttiskannaamalla `nmap -sn`

![kuva1](/H1/kuvat/kuva7.png)

Sammutettuani netin, Ensin käytin vain `nmap -sn` joka antoi vastauksen No targets were specified ja ymmärsin että pitää laittaa IP osoite perään. 

![kuva1](/H1/kuvat/Kuva8.png)

### H) Metasploitable porttiskannaus komennolla `nmap -A -T4 -p-` 

Valitsin portit

Portti 21 Telnet

![kuva1](/H1/kuvat/kuva9.png)

Telnet näyttää salasanat selvässä tekstissä ilman mitään salausta joka tekee siitä haavoittuvaisuuden

Portti 21 FTP

![kuva1](/H1/kuvat/kuva10.png)

Skannauksessa tuli ilmi: Anonymous FTP log in allowed. Antaa luvan anonyyminä ladata ja lukea tiedostoja.'






