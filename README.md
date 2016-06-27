# Bitácora
##Objetivo  
El proyecto consiste en configurar un cluster de raspberry pis para compilación en paralelo 
##Configuración Red
Para el proyecto se configuró una red con ips estáticas para el servidor y para los clientes junto con un switch de DLink como base en topología de estrella:  
Servidor: 192.168.169.101/24  
Cliente1: 192.168.169.102/24  
Cliente2: 192.168.169.103/24  
##Instalar
Cliente:  
nfs-common  
gcc/gfortran  
ssh  
rpcbind  
descargar mpich3.tar.gz  

Servidor:  
nfs-kernel-server  
gcc/gfortran  
ssh  
rpcbind  
descargar mpich3.tar.gz   

##Configurar Red
Modificar archivos de configuración  
```
/etc/network/interfaces
/etc/hosts
/etc/hostname
```

##Configurar NFS
Servidor: Agregar en  
`/etc/exports`

`/home/pi 192.168.169.101/24(rw, no_subtree_check)`

Cliente: Agregar en `/etc/fstab`

`192.168.169.101:/home/pi /home/pi nfs defaults 00`

##Reiniciar servicios
Servidor:  
```
rpcbind
nfs-kernel-server
```

Clientes:  
```
rpcbind
nfs-common
```
##Configurar ssh
Servidor y Cliente  
```
ssh_keygen -t rsa -C "pi@raspberry"
cat /home/pi/.ssh/id_rsa.pub>>/home/pi/.ssh/authorized_keys
```

##Instalar mpich
```
tar -xzvf mpich
./configure
make
sudo make install
export PATH=$PATH:ruta/bin
```

### Servidor 1

Se comenzó con la instalación de los paquetes:

```
aptitude install gcc
aptitude search rcpbind
aptitude search nfs
```

Después la descarga de mpich:

```
wget http://www.mpich.org/static/downloads/3.2/mpich-3.2.tar.gz
```

La configuracion de la red fue la siguiente:

```
vim /etc/network/interfaces
```

```
auto eth0
iface eth0 inet static
address 192.168.169.102
netmask 255.255.255.0
gateway 192.168.169.1
```

Después nos encargamos de configurar el archivo hosts:

```
vim /etc/hosts
```

```
192.168.169.1 carlos
192.168.169.2 jesus
192.168.169.3 cliente
```

Para la configuración del NFS se agrego la siguiente línea a `/etc/fstab`

```
192.168.169.101:/home/pi /home/pi nfs    defaults  0       0
```

Cuando estuvo listo el servicio de NFS se agregó al Path, la ruta de mpich del servidor, pues ya estaba compilado e instalado en su home