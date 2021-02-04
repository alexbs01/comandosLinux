## Cambiar el nombre de los adaptadores de red

Cambiará el nombre de los adaptadores de red, de enp0s3 a eth0 y sucesivos.  
```sh
~$ sudo nano /etc/default/grub
```

```
# En la línea
GRUB_CMDLINE_LINUX=""

# Añadir entre las comillas lo siguiente
GRUB_CMDLINE_LINUX="net.ifnames=0 biosdevnames=0"
```

Luego actualizaremos grub y reiniciaremos la máquina.  
```sh
~$ sudo update-grub
~$ reboot
```

Cuando reinicie podremos comprobar que los nombres cambiaron usando uno de los siguientes comandos.  
```sh
~$ ls /sys/class/net/
~$ ip a
```

## Configuración de red por consola
Se hará utilizando **netplan**, que será una una descripción de los adaptadores de red en un archivo **.yaml**. En un Ubuntu Desktop el .yaml por lo que vi tiene el nombre *01-network-manager-all.yaml*, y en Ubuntu Server tiene el nombre de *50-cloud-init.yaml*.  
En el ejemplo será un servidor con dos interfaces de red.

```sh
~$ sudo nano /etc/netplan/01-network-manager-all.yaml
```

```yaml
# Los corchetes son obligatorios y no se puede indentar con el tabulador, tiene que ser con la barra espaciadora.
network:
  version: 2
  renderer: NetworkManager
  ethernets:
    eth0:
     dhcp4: no
     dhcp6: no
     addresses: [<IP1>/<mascara>]
     gateway4: <IPGateway>
     nameservers:
      addresses: [<DNS1>, <DNS2>]
    eth1:
     dhcp4: no
     dhcp6: no
     addresses: [<IP2>/<mascara>]
```

Para aplicar los cambios de la configuración se ejecutarán los siguientes comandos, el primero para aplicar cambios y ver si hay fallos, y el segundo para que la configuración tenga efecto.  

```sh
~$ sudo netplan --debug generate
~$ sudo netplan apply
```
