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

Kaikki 1000 porttia ovat kiinni

### Demonien asennus ja uudelleen skannaus: 
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
