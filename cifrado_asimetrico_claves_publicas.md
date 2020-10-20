## Tarea 3: Cifrado asimétrico con claves públicas

Tras realizar el ejercicio anterior, podemos enviar ya documentos cifrados utilizando la clave pública de los destinatarios del mensaje.

### 1. Cifraremos un archivo cualquiera y lo remitiremos por email a uno de nuestros compañeros que nos proporcionó su clave pública.

* Creamos el fichero de prueba

```sh
celia@debian:~$ nano tarea_cifrar.txt
celia@debian:~$ cat tarea_cifrar.txt 
Este es un fichero de prueba para una tarea de cifrado.
```

* Lo [ciframos](https://www.genbeta.com/desarrollo/manual-de-gpg-cifra-y-envia-datos-de-forma-segura#:~:text=Para%20poder%20cifrar%20asim%C3%A9tricamente%20primero,comando%20gpg%20%2D%2Dgen%2Dkey%20.&text=GPG%20nos%20permite%20elegir%20el,caso%20usaremos%20DSA%20y%20Elgamal%20.) con la clave pública que hemos importado del compañero.

``` sh
celia@debian:~$ gpg --encrypt --recipient ******************  tarea_cifrar.txt 
```

* Nos dice que no es seguro que la clave pertenezca a la persona nombrada en el ID del usuario. Nosotros sabemos quien nos lo ha enviado así que respondemos con un sí.

```sh 
It is NOT certain that the key belongs to the person named
in the user ID.  If you really know what you are doing,
you may answer the next question with yes.

Use this key anyway? (y/N) y
```
* Lo enviamos al 'compañero'.

### 2. Nuestro compañero, a su vez, nos remitirá un archivo cifrado para que nosotros lo descifremos.

* Descargamos el archivo cifrado del 'compañero'

```sh
celia@debian:~$ ls
celia_garcia.asc  Descargas   Escritorio  Imágenes  Plantillas  tarea_cifrar.txt.gpg
celia.gpg         Documentos  github      Música    Público     Vídeos

```

* Procedemos a descifrar el fichero **tarea_cifrar.txt.gpg** en uno nuevo que vamos a generar **fichero_descifrado.txt**. Usamos la opción decrypt o **-d**. Nos pedirá nuestra clave.


```sh
celia@debian:~$ gpg --output fichero_descifrado.txt -d tarea_cifrar.txt.gpg 
```
salida:
```sh
gpg: cifrado con clave de 3072 bits RSA, ID F819E9D5D89015B9, creada el 2020-10-20
      "Celia Garcia <cgarmai95@gmail.com>"

```

### 3. Tanto nosotros como nuestro compañero comprobaremos que hemos podido descifrar los mensajes recibidos respectivamente.

* Visualizamos el fichero para ver que se ha descifrado correctamente

```sh
celia@debian:~$ cat fichero_descifrado.txt 
Este es un fichero de prueba para una tarea de cifrado.

```

### 4. Por último, enviaremos el documento cifrado a alguien que no estaba en la lista de destinatarios y comprobaremos que este usuario no podrá descifrar este archivo.

* Enviamos el documento a alguien, que no tiene nuestra clave pública y comprobamos que no puede descifrarlo sin nuestra clave pública.

```sh
user@debian:~$ gpg --output fichero.txt -d tarea_cifrar.txt.gpg 
gpg: encrypted with RSA key, ID F819E9D5D89015B9
gpg: decryption failed: No secret key
```


### 5. Para terminar, indica los comandos necesarios para borrar las claves públicas y privadas que posees.

* Para eliminar claves públicas hacemos lo siguiente.

```sh
celia@debian:~$ gpg --delete-key "celia"
gpg (GnuPG) 2.1.18; Copyright (C) 2017 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

pub  rsa3072/507211A95CBA58C8 2020-10-20 Celia Garcia <cgarmai95@gmail.com>

Delete this key from the keyring? (y/N) y
```

* Para eliminar claves privadas

```sh
celia@debian:~$ gpg --delete-secret-key "celia"
gpg (GnuPG) 2.2.12; Copyright (C) 2018 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.


sec  rsa3072/507211A95CBA58C8 2020-10-20 Celia Garcia <cgarmai95@gmail.com>

¿Eliminar esta clave del anillo? (s/N) 

```
