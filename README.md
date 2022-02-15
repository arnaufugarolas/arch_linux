# Arch Linux

## Preparación
#### ⚠️Antes de hacer nada tendrás que deshabilitar el Secure Boot en la BIOS, ya que el instalador de Arch no está firmado.️⚠️

### Primer paso
Tendremos que crear un USB bootable con la ISO oficial de Arch Linux y Rufus, una herramienta para crear un USB bootable.
[ISO Arch](https://mirror.librelabucm.org/archlinux/iso/latest/) && [Rufus](https://rufus.ie/es/)

### Segundo paso
Si queremos instalar Arch juntamente a Windows deberemos dejar el espacio que queremos usar para instalar Arch así facilitaremos la instalación

## Instalación
Iniciaremos el instalador y primero de todo lo que tendremos que hacer es configurar el diseño de teclado, ya que él por defecto carga con la de USA
```
loadkeys es
```
Comprobaremos si tenemos conexión a internet haciendo un ping a Google
```
ping google.com
```
Si no tenemos conexión la tendremos que configurar nosotros, si la manera en la que nos conectamos a internet es vía un cable Ethernet solo tendremos que activar el DHCP
```
dhclient -4
```
