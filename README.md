# Bitácora
##Objetivo  
El proyecto consiste en configurar un cluster de raspberry pis para compilación en paralelo 
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
