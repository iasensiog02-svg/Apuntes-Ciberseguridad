
---

La herramienta de `crunch` es usada para generar una lista de palabras, diccionario, usualmente usada para [[Fuerza Bruta y Cracking de Contraseñas]].

---

## Sintaxis básica

```
crunch <min> <max> <flags>
```

- `<min>` -> longitud mínima.
- `<max>` -> longitud máxima.
- `<flags>` -> Opciones para el crunch.

---

## Flags

- `@` -> letra minúscula
- `,` -> letra mayúscula
- `%` -> Número
- `^` -> Símbolo
- `?` o `+` -> Cualquier carácter del conjunto

Ejemplo:

```
crunch 8 8 -t @@%%%%^^
```

Esto significa que creará una contraseña de 8 caracteres, 2 letras minúsculas, 4 números y 2 símbolos.

---
## Prefijos y sufijos

- `-p` -> Prefijo
- `-s` -> Sufijo

A continuación del prefijo o sufijo se le añadiría una palabra como en este ejemplo:

```
crunch 4 4 abc123 -p inicio
crunch 4 4 abc123 -s fin
```
