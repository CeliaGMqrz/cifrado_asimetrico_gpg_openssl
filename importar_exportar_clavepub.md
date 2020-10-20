## Tarea 2: Importar / exportar clave pública

Para enviar archivos cifrados a otras personas, necesitamos disponer de sus **claves públicas**. De la misma manera, si queremos que cierta persona pueda enviarnos datos cifrados, ésta necesita conocer nuestra clave pública. Para ello, podemos hacérsela llegar por email por ejemplo. Cuando recibamos una clave pública de otra persona, ésta deberemos incluirla en nuestro **keyring** o anillo de claves, que es el lugar donde se almacenan todas las claves públicas de las que disponemos.

### 1. Exporta tu clave pública en formato ASCII y guardalo en un archivo 'nombre_apellido.asc' y envíalo al compañero con el que vas a hacer esta práctica.

* Para enviar una clave pública a alguien, primero tendríamos que **exportarla** con la opción:

```sh
celia@debian:~$ gpg --output celia.gpg --export cgarmai95@gmail.com

``` 
* Al estar en formato binario la clave no es muy segura por lo que para ello vamos a exportarla en formato ASCII. GnuPG ofrece una opción **--armor** que lo hace posible.

```sh
celia@debian:~$ gpg --armor --output celia_garcia.asc --export cgarmai95@gmail.com
```

* **celia_garcia.asc** lo enviamos al correo electrónico de la persona con la que vamos a compartirla. En este caso me lo enviaré a mi otra cuenta de correo electrónico y lo abriré desde un segundo ordenador.


### 2. Importa las claves públicas recibidas de vuestro compañero.

* Vamos a descargar nuestra clave del correo recibido y vamos a proceder a importar la clave pública.

```sh
cgm@debian:~$ ls
cgm_garcia.asc  Escritorio   Imágenes  Plantillas  venv            virtualenv
Descargas         github       logs      Público     Vídeos
Documentos        Grabaciones  Música    sitioweb    VirtualBox VMs
```
```sh
cgm@debian:~$ gpg --import celia_garcia.asc 
gpg: key 507211A95CBA58C8: public key "Celia Garcia <cgarmai95@gmail.com>" imported
gpg: Total number processed: 1
gpg:               imported: 1
```

### 3. Comprueba que las claves se han incluido correctamente en vuestro keyring.

* Vemos que se ha añadido perfectamente a nuestro keyring.

```sh
cgm@debian:~$ gpg --list-keys
/home/cgm/.gnupg/pubring.kbx
------------------------------
pub   rsa3072 2020-10-20 [SC] [expires: 2020-11-19]
      4BB61AF55D2BBA02B311F8AF507211A95CBA58C8
uid           [ unknown] Celia Garcia <cgarmai95@gmail.com>
sub   rsa3072 2020-10-20 [E] [expires: 2022-10-20]
```

