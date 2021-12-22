
# Instalation of an ArchLinux machine

## Pre-Instalation 

First of all we have to set our keyboard so we do this:

- Spanish keyboard setup

```sh
loadkeys es
```

- Connect to internet:

Make sure that you have an ip adress assigned and a network interface is UP

```sh
ip a
```
TO DO (SALIDA COMANDO)

```sh
ping archlinux.org
```
TO DO (SALIDA COMANDO)

- Disk preparation

```sh
cfdisk /dev/sdX
```
Where X is the hard drive

-select gpt partition table

-despres 2 particions on una de 24G (ext4 (83)), 1G (linux (82) swap)

-Finalment write (yes teclejar tot) per confirmar canvis

-quit

-  Update the system clock
```sh
timedatectl set-ntp true
```
To check the sevice status, use: 
```
timedatectl status
```
- Partition the disks 

To see our partitions whe do:

```sh
fdisk -l
```
Then format the partitions

- Formating partitions

Root partition (/), type Ext4
```sh
mkfs.ext4 /dev/root_partition
```
Were root_partition is sda1, sda2, ...

Swap
```sh
mkswap /dev/swap_partition
```
Finally we mount our disk

- Mounting the disk:

```sh
mount /dev/root_partition /mnt
```
- Mounting the swap:
```sh
swapon /dev/swap_partition
```
## Select the mirrors

To do (opcional)

## Essential Packages

```sh
pacstrap /mnt base linux linux-firmware nano
```
## Configure the system

### Fstab

Generate an fstab file (use -U or -L to define by UUID or labels, respectively):

```sh
genfstab -U /mnt >> /mnt/etc/fstab
```

Check the resulting /mnt/etc/fstab file, and edit it in case of errors.
Chroot

Change root into the new system:
```sh
arch-chroot /mnt
```

### Time zone

Set the time zone:
```sh
ln -sf /usr/share/zoneinfo/Region/City /etc/localtime
```

Run hwclock to generate /etc/adjtime:

```sh
hwclock --systohc
```
Ths command assumes the hardware clock is set to UTC. See System time#Time standard for details.

### Localization

Edit /etc/locale.gen and uncomment en_US.UTF-8 UTF-8 and other needed locales. Generate the locales by running:
```sh
locale-gen
```
