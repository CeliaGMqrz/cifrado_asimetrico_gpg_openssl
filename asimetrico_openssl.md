## Cifrado asimétrico con openssl

## Tarea 5: Cifrado asimétrico con openssl

En esta ocasión vamos a cifrar nuestros ficheros de forma asimétrica utilizando la herramienta **openssl**.

### 1. Genera un par de claves (pública y privada).

* Para generar un par de claves RSA pública y privada que nos permitan tando cifrar datos como realizar firmas se emplea el siguiente comando:

```sh
celia@debian:~$ openssl genrsa -out localhost.key 8192
Generating RSA private key, 8192 bit long modulus (2 primes)
.......................................................................................+++
..........+++
e is 65537 (0x010001)
celia@debian:~$ ls
celia_garcia.asc  Documentos              github         Música      tarea_cifrar.txt.gpg
celia.gpg         Escritorio              Imágenes       Plantillas  Vídeos
Descargas         fichero_descifrado.txt  localhost.key  Público

```
* Pero vamos a crearlas con el formato .pem

```sh
celia@debian:~$ openssl genrsa -out key.pem 4096
Generating RSA private key, 4096 bit long modulus (2 primes)
...................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................................++++
...++++
e is 65537 (0x010001)
celia@debian:~$ openssl rsa -in key.pem -out key.pub.pem -outform PEM -pubout
writing RSA key

```
### 2. Envía tu clave pública a un compañero.

*  Se lo enviamos al 'compañero'.

### 3. Utilizando la clave pública cifra un fichero de texto y envíalo a tu compañero.

* Ciframos un fichero de texto con la clave pública

```sh

$ openssl rand -base64 48 -out key.txt

$ openssl enc -aes-256-cbc -pass file:key.txt -in fichero.txt -out fichero_cifrado.encrypted

$ openssl rsautl -encrypt -in key.txt -out key.enc -inkey key.pub.pem -pubin
```

### 4. Tu compañero te ha mandado un fichero cifrado, muestra el proceso para el descifrado.

```sh

$ openssl rsautl -decrypt -inkey ./clave.pem -in key.enc -out key.txt

$ openssl enc -aes-256-cbc -d -pass file:key.txt -in fichero_cifrado.encrypted -out fichero.txt
```