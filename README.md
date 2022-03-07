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
EL siguiente passo es encongtarr el nombre del disco que usaremos para hacer la instalacion
```
lsblk -o NAME,KNAME,SIZE
```
Una vez sepamos el disco crearemos 2 particiones una de 512M para ell boot y una de el espacio que queramos darle al sistema operativo
```
cfdisk /dev/disco
```
Una vez tengamos creada la partcion del S.O. la encriptaremos
```
cryptsetup --type luks2 --cipher aes-xts-plain64 --key-size 512 --hash sha512 --iter-time 2000 --pbkdf argon2id --use-urandom --verify-passphrase luksFormat /dev/ParticionRoot
```
Una vez lo tengamos encriptado tendrmeo que abrirlo
```
cryptsetup luksOpen /dev/sda2 luks
```

```
pvcreate /dev/mapper/luks
vgcreate vg0 /dev/mapper/luks
```

```
lvcreate -l +90%FREE vg0 -n root
lvcreate -l +100%FREE vg0 -n swap
```

```
mkfs.fat -F 32 /dev/sda1
mkswap /dev/vg0/swap
mkfs.ext4 /dev/vg0/root
```

```
mount /dev/vg0/root /mnt
mkdir /mnt/boot
mount /dev/sda1 /mnt/boot
swapon /dev/vg0/swap
```
