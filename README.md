# Arch Linux

## Preparación
#### ⚠️Antes de hacer nada tendrás que deshabilitar el Secure Boot en la BIOS, ya que el instalador de Arch no está firmado.️⚠️

### Primer paso
Tendremos que crear un USB bootable con la ISO oficial de Arch Linux y Rufus, una herramienta para crear un USB bootable.
[ISO Arch](https://mirror.librelabucm.org/archlinux/iso/latest/) && [Rufus](https://rufus.ie/es/)

### Segundo paso
Si queremos instalar Arch juntamente a Windows deberemos dejar el espacio que queremos usar para instalar Arch así facilitaremos la instalación.

### Previa
Iniciaremos el instalador y primero de todo lo que tendremos que hacer es configurar el diseño de teclado, ya que él por defecto carga con la de USA.
```
loadkeys es
```

Comprobaremos si tenemos conexión a internet haciendo un ping a Google.
```
ping google.com
```

Si no tenemos conexión la tendremos que configurar nosotros, si la manera en la que nos conectamos a internet es vía un cable Ethernet solo tendremos que activar el DHCP.
```
dhclient -4
```

Si nuestro dispositivo va via WiFi tendremos que comprovar que interfice de red tenemos ejecutando el segundo comando, la interfice del WiFI sera la 2nda.
```
ip link
```

Para poder conectarnos a una red via WiFi tendrmeos que desabilitar el RF-KILL
```
rfkill unblock all
```

Una vez tengamos la inteficie de red tendremos que conectarnos a nuestro WiFi
```
iwctl --passphrase CONTRASEÑA station INTERFICIE connect NOMBRE_RED
```

Volveremos a hacer un ping para comprovar si tenemos conexion, si tenemos conexion podremos emepzar con la instalacion.

## Instalación
Primero de todo configuraremos la hora actumatica para prevenir posibles errores
```
timedatectl set-timezone Europe/Madrid
timedatectl set-ntp true
```
