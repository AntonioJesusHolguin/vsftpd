# VSFTPD
## Índice

1. [Introducción](#int)
2. [Comparativa con proftpd](#com)
3. [Esquema de red](#esq)
4. [Instalación](#ins)
5. [Casos prácticos](#cas)
6. [Referencias](#ref)

<a name="int"></a>
## 1.- Introducción

En este repositorio vamos a ver qué es y como podemos implementar vsftpd en nuestro servidor de Debian. Este servicio permitirá a los usuarios establecer una conexión con el servidor para mover, copiar o modificar ficheros, entre otros.

<a name="com"></a>
## 2.- Comparativa con proftpd

Vsftpd comparte similitudes con proftpd, otro servidor ftp muy popular en distribuciones de linux. Sin embargo, nos encontramos con particularidades, por ejemplo, vstfpd se aloja en /etc/ , mientras que proftpd tiene su propio directorio: /etc/proftpd/.

<a name="esq"></a>
## 3.- Esquema de red

Para este proyecto, requeriremos únicamente de un servidor Debian y un cliente que formen parte de la misma red, en mi caso, dicha red es la 192.168.2.0/24.

Vamos a configurar la IP de nuestro servidor y de nuestro cliente, primeros nos logueamos como root y escribimos los siguientes comandos:

Desactivamos NetworkManager (Solo necesario para sistemas Debian con interfaz gráfica):
```
systemctl stop NetworkManager
systemctl disable NetworkManager
```
Accedemos a /etc/network/interfaces y editamos el fichero de la siguiente forma para el servidor:
```
source /etc/network/interfaces.d/*

# The loopback network interface
auto lo
iface lo inet loopback

# El nombre de mi adaptador de red es enp0s3, recordemos comprobar el nombre
auto enp0s3
iface enp0s3 inet static
address 192.168.2.56
netmask 255.255.255.0
broadcast 192.168.2.255
network 192.168.2.0
gateway 192.168.2.1
```
A continuación, para el cliente:
```
iface enp0s3 inet static
address 192.168.2.10
netmask 255.255.255.0
broadcast 192.168.2.255
network 192.168.2.0
gateway 192.168.2.1
```

<a name="ins"></a>
## 4.- Instalación

Ahora que tenemos configurado nuestro esquema de red, podremos pasar a la instalación de vsftpd. Para ello, solo debemos ejecutar el siguiente comando:

```
apt-get install vsftpd
```

Una vez finalice la instalación, podemos encontrar los ficheros de configuración que usaremos en /etc/. Para asegurarnos de que la el servicio funciona, ejecutaremos el siguiente comando:

```
systemctl status vsftpd
```

<a name="cas"></a>
## 5.- Casos prácticos
Si el servicio funciona correctamente, estaremos listos para pasar a los casos practicos que veremos a continuación.

1.- Versión de vsftpd instalada:

```
vsftpd -version
```

### 2.- Usuarios creados en la instalación

En FTP podemos distinguir a los usuarios físicos del servidor y a los usuarios virtuales. Aunque todavía no tenemos ningun usuario virtual, podremos ver que se nos ha creado un usuario físico en el servidor llamado ftp. Podemos ver a dicho usuario con el siguiente comando:

```
cat /etc/passwd
```
### 3.- Ficheros de configuración

Vsftpd no tiene una carpeta con todos sus archivos de configuración. Veremos que el principal fichero es vsftpd.conf el cual se encuentra dentro de /etc/.

### 4.- Acceso al servidor FTP: usuarios del sistema.

### 5.- Acceso al servidor FTP: anónimo tiene solo permiso de lectura en su directorio de trabajo.

### 6.- Acceso al servidor FTP: anónimo tiene permiso de escritura en el directorio sugerencias, que es un subdirectorio de su directorio raíz.

### 7.- Acceso al servidor FTP: Creación de usuarios virtuales.

### 8.- Acceso seguro al servidor FTP

<a name="ref"></a>
## 6.- Referencias

- [www.howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-and-configure-vsftpd/)
- []
