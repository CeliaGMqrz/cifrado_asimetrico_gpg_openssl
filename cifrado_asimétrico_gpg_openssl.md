## Tarea 1: Generación de claves.

Los algoritmos de cifrado asimétrico utilizan dos claves para el cifrado y descifrado de mensajes. Cada persona involucrada (receptor y emisor) debe disponer, por tanto, de una pareja de claves pública y privada. Para generar nuestra pareja de claves con gpg utilizamos la opción --gen-key:

Para esta práctica no es necesario que indiquemos frase de paso en la generación de las claves (al menos para la clave pública).

### 1. Genera un par de claves (pública y privada). ¿En que directorio se guarda las claves de un usuario?

Generamos el par de claves con **gpg --gen-key**. Nos pedirá el Nombre, los apellidos y la dirección de correo electrónico. Además de una clave para encriptarla que debe de tener al menos un carácter especial para que sea más segura.

```sh
celia@debian:~$ gpg --gen-key
```

Salida:

``` sh
gpg (GnuPG) 2.2.12; Copyright (C) 2018 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Nota: Usa "gpg --full-generate-key" para el diálogo completo de generación de clave.

GnuPG debe construir un ID de usuario para identificar su clave.

Nombre y apellidos: Celia Garcia
Dirección de correo electrónico: cgarmai95@gmail.com
Ha seleccionado este ID de usuario:
    "Celia Garcia <cgarmai95@gmail.com>"

¿Cambia (N)ombre, (D)irección o (V)ale/(S)alir? v
Es necesario generar muchos bytes aleatorios. Es una buena idea realizar
alguna otra tarea (trabajar en otra ventana/consola, mover el ratón, usar
la red y los discos) durante la generación de números primos. Esto da al
generador de números aleatorios mayor oportunidad de recoger suficiente
entropía.
Es necesario generar muchos bytes aleatorios. Es una buena idea realizar
alguna otra tarea (trabajar en otra ventana/consola, mover el ratón, usar
la red y los discos) durante la generación de números primos. Esto da al
generador de números aleatorios mayor oportunidad de recoger suficiente
entropía.
gpg: clave 507211A95CBA58C8 marcada como de confianza absoluta
gpg: creado el directorio '/home/celia/.gnupg/openpgp-revocs.d'
gpg: certificado de revocación guardado como '/home/celia/.gnupg/openpgp-revocs.d/4BB61AF55D2BBA02B311F8AF507211A95CBA58C8.rev'
claves pública y secreta creadas y firmadas.

pub   rsa3072 2020-10-20 [SC] [caduca: 2022-10-20]
      4BB61AF55D2BBA02B311F8AF507211A95CBA58C8
uid                      Celia Garcia <cgarmai95@gmail.com>
sub   rsa3072 2020-10-20 [E] [caduca: 2022-10-20]

```

El directorio donde se guardan es **.gnupg**.

```sh
celia@debian:~$ cd .gnupg/
celia@debian:~/.gnupg$ ls
openpgp-revocs.d  private-keys-v1.d  pubring.kbx  pubring.kbx~  trustdb.gpg

```

### 2. Lista las claves públicas que tienes en tu almacén de claves. Explica los distintos datos que nos muestra. ¿Cómo deberías haber generado las claves para indicar, por ejemplo, que tenga un 1 mes de validez?

* Para listar las claves ejecutamos:

```sh
celia@debian:~$ gpg --list-keys
```
* Este comando nos enumera las claves públicas que tnemos, nos dice la validez, la confianza y si está firmada. Nos dice que la siguiente comprobación de confianza donde se nos pedirá la clave nuevamente será dentro de dos años. Es decir, que la clave **tiene una validez de dos años**.

Salida:

```sh 
gpg: comprobando base de datos de confianza
gpg: marginals needed: 3  completes needed: 1  trust model: pgp
gpg: nivel: 0  validez:   1  firmada:   0  confianza: 0-, 0q, 0n, 0m, 0f, 1u
gpg: siguiente comprobación de base de datos de confianza el: 2022-10-20
/home/celia/.gnupg/pubring.kbx
------------------------------
pub   rsa3072 2020-10-20 [SC] [caduca: 2022-10-20]
      4BB61AF55D2BBA02B311F8AF507211A95CBA58C8
uid        [  absoluta ] Celia Garcia <cgarmai95@gmail.com>
sub   rsa3072 2020-10-20 [E] [caduca: 2022-10-20]

```
* Para generar una clave que tenga un mes de validez ejecutamos gpg pero con todas las caracteristicas con este comando 

```sh
celia@debian:~$ gpg --full-generate-key
```

* Nos pide el tipo de clave que queremos crear, el tamaño de la clave, la validez (que en este caso hemos puesto 1 mes), y después los datos personales del propietario de la clave con su contraseña para encriptar.

Salida: 
```sh
gpg (GnuPG) 2.2.12; Copyright (C) 2018 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Por favor seleccione tipo de clave deseado:
   (1) RSA y RSA (por defecto)
   (2) DSA y ElGamal
   (3) DSA (sólo firmar)
   (4) RSA (sólo firmar)
Su elección: 
las claves RSA pueden tener entre 1024 y 4096 bits de longitud.
¿De qué tamaño quiere la clave? (3072) 
El tamaño requerido es de 3072 bits
Por favor, especifique el período de validez de la clave.
         0 = la clave nunca caduca
      <n>  = la clave caduca en n días
      <n>w = la clave caduca en n semanas
      <n>m = la clave caduca en n meses
      <n>y = la clave caduca en n años
¿Validez de la clave (0)? 1m
La clave caduca jue 19 nov 2020 16:38:50 CET
¿Es correcto? (s/n) s

GnuPG debe construir un ID de usuario para identificar su clave.

Nombre y apellidos: Celia García
Dirección de correo electrónico: cgarmai95@hotmail.com
Comentario: 
Está usando el juego de caracteres 'utf-8'.
Ha seleccionado este ID de usuario:
    "Celia García <cgarmai95@hotmail.com>"

¿Cambia (N)ombre, (C)omentario, (D)irección o (V)ale/(S)alir? v
Es necesario generar muchos bytes aleatorios. Es una buena idea realizar
alguna otra tarea (trabajar en otra ventana/consola, mover el ratón, usar
la red y los discos) durante la generación de números primos. Esto da al
generador de números aleatorios mayor oportunidad de recoger suficiente
entropía.
Es necesario generar muchos bytes aleatorios. Es una buena idea realizar
alguna otra tarea (trabajar en otra ventana/consola, mover el ratón, usar
la red y los discos) durante la generación de números primos. Esto da al
generador de números aleatorios mayor oportunidad de recoger suficiente
entropía.
gpg: clave 7966424A3ADC5869 marcada como de confianza absoluta
gpg: certificado de revocación guardado como '/home/celia/.gnupg/openpgp-revocs.d/A5964C8082FC74635474E9DD7966424A3ADC5869.rev'
claves pública y secreta creadas y firmadas.

pub   rsa3072 2020-10-20 [SC] [caduca: 2020-11-19]
      A5964C8082FC74635474E9DD7966424A3ADC5869
uid                      Celia García <cgarmai95@hotmail.com>
sub   rsa3072 2020-10-20 [E] [caduca: 2020-11-19]


```

* También podríamos editar la validez de la clave con el comando **gpg --key-edit**, pero antes deberemos listar las claves para saber el nombre de la que queremos editar.

```sh
celia@debian:~$ gpg --list-key
```

Salida:

```sh

gpg: comprobando base de datos de confianza
gpg: marginals needed: 3  completes needed: 1  trust model: pgp
gpg: nivel: 0  validez:   2  firmada:   0  confianza: 0-, 0q, 0n, 0m, 0f, 2u
gpg: siguiente comprobación de base de datos de confianza el: 2020-11-19
/home/celia/.gnupg/pubring.kbx
------------------------------
pub   rsa3072 2020-10-20 [SC] [caduca: 2022-10-20]
      4BB61AF55D2BBA02B311F8AF507211A95CBA58C8
uid        [  absoluta ] Celia Garcia <cgarmai95@gmail.com>
sub   rsa3072 2020-10-20 [E] [caduca: 2022-10-20]

pub   rsa3072 2020-10-20 [SC] [caduca: 2020-11-19]
      A5964C8082FC74635474E9DD7966424A3ADC5869
uid        [  absoluta ] Celia García <cgarmai95@hotmail.com>
sub   rsa3072 2020-10-20 [E] [caduca: 2020-11-19]

```
* Ponemos el nombre de la clave y le decimos a gpg **expire** para cambiar la caducidad, y depués con **save** aplicamos los cambios y salimos.

```sh
celia@debian:~$ gpg --key-edit 4BB61AF55D2BBA02B311F8AF507211A95CBA58C8
gpg (GnuPG) 2.2.12; Copyright (C) 2018 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Clave secreta disponible.

sec  rsa3072/507211A95CBA58C8
     creado: 2020-10-20  caduca: 2022-10-20  uso: SC  
     confianza: absoluta      validez: absoluta
ssb  rsa3072/F819E9D5D89015B9
     creado: 2020-10-20  caduca: 2022-10-20  uso: E   
[  absoluta ] (1). Celia Garcia <cgarmai95@gmail.com>

gpg> expire
Cambiando caducidad de clave primaria.
Por favor, especifique el período de validez de la clave.
         0 = la clave nunca caduca
      <n>  = la clave caduca en n días
      <n>w = la clave caduca en n semanas
      <n>m = la clave caduca en n meses
      <n>y = la clave caduca en n años
¿Validez de la clave (0)? 1m
La clave caduca jue 19 nov 2020 16:44:54 CET
¿Es correcto? (s/n) s

sec  rsa3072/507211A95CBA58C8
     creado: 2020-10-20  caduca: 2020-11-19  uso: SC  
     confianza: absoluta      validez: absoluta
ssb  rsa3072/F819E9D5D89015B9
     creado: 2020-10-20  caduca: 2022-10-20  uso: E   
[  absoluta ] (1). Celia Garcia <cgarmai95@gmail.com>

gpg> save
```

### 3. Lista las claves privadas de tu almacén de claves.

* Listamos las claves privadas de igual manera que las publicas pasándole el parámetro secret.

```sh
celia@debian:~$ gpg --list-secret-keys
gpg: comprobando base de datos de confianza
gpg: marginals needed: 3  completes needed: 1  trust model: pgp
gpg: nivel: 0  validez:   2  firmada:   0  confianza: 0-, 0q, 0n, 0m, 0f, 2u
gpg: siguiente comprobación de base de datos de confianza el: 2020-11-19
/home/celia/.gnupg/pubring.kbx
------------------------------
sec   rsa3072 2020-10-20 [SC] [caduca: 2020-11-19]
      4BB61AF55D2BBA02B311F8AF507211A95CBA58C8
uid        [  absoluta ] Celia Garcia <cgarmai95@gmail.com>
ssb   rsa3072 2020-10-20 [E] [caduca: 2022-10-20]

sec   rsa3072 2020-10-20 [SC] [caduca: 2020-11-19]
      A5964C8082FC74635474E9DD7966424A3ADC5869
uid        [  absoluta ] Celia García <cgarmai95@hotmail.com>
ssb   rsa3072 2020-10-20 [E] [caduca: 2020-11-19]

```


