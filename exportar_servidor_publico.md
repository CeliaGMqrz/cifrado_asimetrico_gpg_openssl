## Tarea 4: Exportar clave a un servidor público de claves PGP

Para distribuir las claves públicas es mucho más habitual utilizar un servidor específico para distribuirlas, que permite a los clientes añadir las claves públicas a sus anillos de forma mucho más sencilla.


### 1. Genera la clave de revocación de tu clave pública para utilizarla en caso de que haya problemas.

* Utilizamos **gpg --gen-revoke** y el nombre de nuestra clave. Nos preguntará el motivo de la revocación. Si no le indicamos directorio el certificado se crea por defecto en 
**~/.gnupg/openpgp-revocs.d** , con la extensión **rev**.

```sh
celia@debian:~$ gpg --gen-revoke A5964C8082FC74635474E9DD7966424A3ADC5869

sec  rsa3072/7966424A3ADC5869 2020-10-20 Celia García <cgarmai95@hotmail.com>

¿Crear un certificado de revocación para esta clave? (s/N) s
Por favor elija una razón para la revocación:
  0 = No se dio ninguna razón
  1 = La clave ha sido comprometida
  2 = La clave ha sido reemplazada
  3 = La clave ya no está en uso
  Q = Cancelar
(Probablemente quería seleccionar 1 aquí)
¿Su decisión? 2
Introduzca una descripción opcional; acábela con una línea vacía:
> 
Razón para la revocación: La clave ha sido reemplazada
(No se dió descripción)
¿Es correcto? (s/N) s
se fuerza salida con armadura ASCII.
-----BEGIN PGP PUBLIC KEY BLOCK-----
Comment: This is a revocation certificate

iQG2BCABCgAgFiEEpZZMgIL8dGNUdOndeWZCSjrcWGkFAl+PH6UCHQEACgkQeWZC
SjrcWGm/9Qv/ZhlvNKk/PIS3yWsP7TGvc6fV0uLxD1x7c4nfc+PwxSsQffIxCjCh
6lP8WBzdf4pFzjxk4iwCEN5/TKcB15xFc21WQotJ2yHo0IBBxv1HWRJdbeopLacf
CxFxD+qu3/O4rJiboaI72GWiwyhFkEa/vByJW48uO5fjfp7XOA0fjIRdiPN4Ws7y
HspXWPpyCbsgO9lXnau+ay7t4qhboDEhhMt5k8YXg5oXhHRNyhMKuB5e5g2zrdIu
IM2DwS9ma26DZlbEkaE4ZQ7/duxuQ1H1FGyWTtT8tnP3WhmZVGqQcsjr2TSF0cnx
SHlrW9VgWdijc4voFK3UivTWo8p6Vl8K7BxGvga7qbjx1PTmmOOlSjTnFFKWlHZS
jKc4ZpuIdTUfargfjTq1suUsPmAFVMcpPsfDpV9A/QGrKl03BkikESZ2N5BVrRSU
5Q4UF3muG3HHGen6RLT7NBT3A+Wij44wsoCv701YQwtGt9769G4hSlYfU8GJuaoK
WhubHdEx2uEf
=nmX/
-----END PGP PUBLIC KEY BLOCK-----
Certificado de revocación creado.

Por favor consérvelo en un medio que pueda esconder; si alguien consigue
acceso a este certificado puede usarlo para inutilizar su clave.
Es inteligente imprimir este certificado y guardarlo en otro lugar, por
si acaso su medio resulta imposible de leer. Pero precaución: ¡el sistema
de impresión de su máquina podría almacenar los datos y hacerlos accesibles
a otras personas!

```

### 2. Exporta tu clave pública al servidor pgp.rediris.es


* Para subirlo utilizamos el siguiente comando:

```sh
celia@debian:~$ gpg --keyserver pgp.rediris.es --send-key 4BB61AF55D2BBA02B311F8AF507211A95CBA58C8
```
Salida:
```sh
gpg: enviando clave 507211A95CBA58C8 a hkp://pgp.rediris.es

```

### 3. Borra la clave pública de alguno de tus compañeros de clase e impórtala ahora del servidor público de rediris.

* Borrar la clave del 'compañero'

```sh
celia@debian:~$ gpg --delete-key "celia"
gpg (GnuPG) 2.1.18; Copyright (C) 2017 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

pub  rsa3072/507211A95CBA58C8 2020-10-20 Celia Garcia <cgarmai95@gmail.com>

Delete this key from the keyring? (y/N) y

```
* Importamos desde el servidor rediris.

```sh
celia@debian:~$ gpg --keyserver pgp.rediris.es --recv-keys 4BB61AF55D2BBA02B311F8AF507211A95CBA58C8
gpg: key 507211A95CBA58C8: public key "Celia Garcia <cgarmai95@gmail.com>" imported
gpg: Total number processed: 1
gpg:               imported: 1
```