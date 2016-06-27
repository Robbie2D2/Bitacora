# Bitácora
##Objetivo  
El proyecto consiste en configurar un cluster de raspberry pis para compilación en paralelo 
##Configuración Red
Para el proyecto se configuró una red con ips estáticas para el servidor y para los clientes junto con un switch de DLink como base en topología de estrella:  
Servidor: 192.168.169.101  
Cliente1: 192.168.169.102  
Cliente2: 192.168.169.103  
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

`/home/pi red/24(rw, no_subtree_check)`

Cliente: Agregar en `/etc/fstab`

`IP_Serv:/home/pi /home/pi nfs defaults 00`

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
