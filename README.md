# Linux
En este repositorio estarán los distintos comandos que realicé en Linux durante prácticas de clase.

## Comando para instalar las Guest Additions de VBox

Si la instalación de las Guest Additions de VirtualBox falla, se puede solucionar instalando los siguientes paquetes.  

```sh 
sudo apt install linux-headers-$(uname -r) build-essential dkms
```

