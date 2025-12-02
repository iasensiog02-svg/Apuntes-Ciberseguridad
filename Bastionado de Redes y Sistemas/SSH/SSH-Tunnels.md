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


