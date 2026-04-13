Sirve para crear una **conexión segura** entre un ordenador y otro de manera cifrada

---
## Comandos 
<<<<<<< HEAD:Bastionado de Redes y Sistemas/Administración/SSH/SSH-Tunnels.md
---
### Local Port Forwarding 

Local Port Forwarding hace que **un puerto de TU máquina local** actúe como un túnel hacia **un puerto de la máquina remota** a través de SSH..

```
ssh -L localhost:5000:localhost:80 root@<IP> -fN
```

Explicación:
- `localhost:5000` -> puerto local donde escucha mi máquina.
- `localhost:80` -> puerto de la máquina remota al que se conectará el servicio SSH remoto.
- `root@<IP>` -> máquina remota a la que te conectas.

Todo el tráfico que envíes a `localhost:5000` en tu máquina **viaja por el túnel SSH** y llega al **puerto 80 de la máquina remota**

---
### Remote Port Forwarding

Abre un puerto en la **máquina remota**, y cualquier conexión a ese puerto se redirige hacia **un puerto en tu máquina local** a través del túnel SSH.


```
ssh -R 0.0.0.0:7777:localhost:80 <usuario>@<IP> -fN
```

Explicación:
- En la máquina remota, se abre el puerto `7777`.
- Cualquiera que se conecta a `<maquina_remota>:7777` vieja por el túnel, llega al puerto `80` de tu máquina local.
- `0.0.0.0` el puerto remoto queda accesible desde cualquier IP

En el servidor remoto habilitar estas opciones en el fichero `/etc/ssh/sshd_config`:

```
GatewayPorts yes
AllowTcpForwarding yes
```

### Entendimiento final:

- **Local Port Forwarding**: “Yo (cliente) abro un puerto local que apunta a un puerto remoto.”
- **Remote Port Forwarding**: “La máquina remota abre un puerto remoto que apunta a un puerto local mío.”

=======

### Local Port Forwarding 

Esto estaría trayendo el localhost del puerto 80 que seria http al localhost de tu maquina en el puerto 5000.

```
ssh -L localhost:5000:localhost:80 root@maquina -fN
```

Si traes otro tipo de servicio por ejemplo mysql seria el primer local host con la ip de mysql local que seria 127.0.0.1

---

### Remote  Port Forwarding

Para que esto funcione se necesita realizar un cambio en lo el fichero `/etc/ssh/sshd_config`

![[Pasted image 20251202202106.png]]

Abre un puerto en la maquina remota que apunta a un puerto de tu maquina local.

Explicación:
- En la máquina remota, el puerto 7777 queda abierto.
- Todo lo que llegue va al puerto 80 de tu maquina local
- Si se usa 0.0.0.0, entonces con ese puerto queda accesible desde cualquier IP.


```
ssh -R 0.0.0.0:7777:localhost:80 root@maquina -fN
```

>>>>>>> 9c04ca7d3b7bf57f962e5a68c144519c140232ae:Bastionado de Redes y Sistemas/SSH/SSH-Tunnels.md
---
### Ver túneles activos

```
ps aux | grep ssh
```

---
### Borrar túneles

<<<<<<< HEAD:Bastionado de Redes y Sistemas/Administración/SSH/SSH-Tunnels.md
Borrar un túnel:
=======
Borrar un túnel
>>>>>>> 9c04ca7d3b7bf57f962e5a68c144519c140232ae:Bastionado de Redes y Sistemas/SSH/SSH-Tunnels.md

```
kill id
```

<<<<<<< HEAD:Bastionado de Redes y Sistemas/Administración/SSH/SSH-Tunnels.md
La `id` 

Para borrar todos los túneles:
=======
Para borrar todos los túneles
>>>>>>> 9c04ca7d3b7bf57f962e5a68c144519c140232ae:Bastionado de Redes y Sistemas/SSH/SSH-Tunnels.md

```
pkill ssh
```


