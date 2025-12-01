
Es una herramienta de [[Fuerza Bruta y Cracking de Contraseñas]] y ataques de diccionario.

---

### Flags

- `-l` -> Un solo usuario.
- `-L` -> Lista de usuarios.
- `-p` -> Una sola contraseña.
- `-P` -> Diccionario de contraseñas.
- `-V` -> verbose.
- `-Vv` -> Muestra mucha información
- `-f` -> Parar al encontrar un login válido.
- `-s` -> Indicar el puerto.
- `-t` -> Número de hilos, recomendable usar el 64

---
### Ejemplos:

Comando básico:

```
hydra -l <usuario> -P <fichero de contraseñas> <IP> <protocolo> <flags>
```

SSH:

```
hydra -l <usuario> -P <fichero de contraseñas> <IP> ssh <flags>
```

FTP:

```
hydra -l <usuario> -P <fichero de contraseñas> <IP> ftp <flags>
```

HTTP POST form:

```
hydra -l <usuario> -P  <fichero de contraseñas> http-post-form://[IP]/login.php:username=^USER^&password=^PASS^:F=Incorrecto
```

MySQL:

```
hydra -l <usuario> -P <fichero de contraseñas> <IP> mysql <flags>
```

Empieza la fuerza bruta a partir de donde dejo la anterior sesión, tiene que ejecutarse en la misma carpeta que el `hydra.restore`.

```
hydra -R
```
