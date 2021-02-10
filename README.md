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

Vsftpd comparte similitudes con proftpd, otro servidor ftp muy popular en distribuciones de linux. Vstfpd se aloja tambien en /etc/ con el nombre vsftpd, donde encontraremos

<a name="esq"></a>
## 3.- Esquema de red

Para este proyecto, requeriremos únicamente de un servidor Debian y un cliente que formen parte de la misma red, en mi caso, dicha red es la 192.168.3.

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
address 192.168.3.1
netmask 255.255.255.0
broadcast 192.168.3.255
network 192.168.3.0
```
A continuación, para el cliente:
```
iface enp0s3 inet static
address 192.168.3.10
netmask 255.255.255.0
broadcast 192.168.3.255
network 192.168.3.0
gateway 192.168.3.1
```

<a name="ins"></a>
## 4.- Instalación

Ahora que tenemos configurado nuestro esquema de red, podremos pasar a la instalación de vsftpd. Para ello, solo debemos ejecutar el siguiente comando:

```
apt-get install vsftpd
```

Una vez finalice la instalación, podemos encontrar los ficheros de configuración que usaremos en /etc/vsftpd/. Para asegurarnos de que la el servicio funciona, ejecutaremos el siguiente comando:

```
systemctl status vsftpd
```

<a name="cas"></a>
## 5.- Casos prácticos
Si el servicio funciona correctamente, estaremos listos para pasar a los casos practicos que veremos a continuación.

1.- Versión de vsftpd instalada:

```

```

2.- Usuarios creados en la instalación

3.-

4.-

5.-

6.-


<a name="ref"></a>
## 6.- Referencias

- [www.howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-and-configure-vsftpd/)
- []
