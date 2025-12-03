Sirve para crear una **conexión segura** entre un ordenador y otro de manera cifrada

---
## Comandos 

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

---
### Ver túneles activos

```
ps aux | grep ssh
```

---
### Borrar túneles

Borrar un túnel

```
kill id
```

Para borrar todos los túneles

```
pkill ssh
```


