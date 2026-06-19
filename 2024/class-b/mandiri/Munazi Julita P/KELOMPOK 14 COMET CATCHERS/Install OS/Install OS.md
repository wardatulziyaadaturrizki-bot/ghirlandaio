## Menghubungkan ke Internet
```
iwctl
device list
station wlan0 scan
station wlan0 get-network
station wlan0 connect “nama wifi”
exit
```

## Cek Jaringan
```
ping 8.8.8.8
```

## Mengaktifkan asciinema
```
asciinema rec nama.cast
```

## LUKS
```
cryptsetup luksFormat /dev/partisi sistem
cryptsetup luksOpen /dev/partisi sistem proc
```

## Cek partisi
```
lsblk
```

## Membuat logical volume
```
pvcreate /dev/mapper/proc
vgcreate [nama volume grup] /dev/mapper/proc
lvcreate -L 8G comet -n root
lvcreate -L 5G comet -n vars
lvcreate -L 1G comet -n vlog
lvcreate -L 1G comet -n vaud
lvcreate -L 1.5G comet -n vtmp
lvcreate -l50%FREE comet -n home
lvcreate -l100%FREE comet -n podman
```

## Cek partisi
```
lsblk
```

## Format partisi
```
mkfs.vfat -F32 /dev/partisi boot
mkfs.ext4 /dev/comet/root
mkfs.ext4 /dev/comet/vars
mkfs.ext4 /dev/comet/vlog
mkfs.ext4 /dev/comet/vaud
mkfs.ext4 /dev/comet/vtmp
mkfs.ext4 /dev/comet/home
mkfs.ext4 /dev/comet/podman
```

## Mounting
```
mount /dev/comet/root /mnt
mount –mkdir -o uid=0,gid=0,fmask=0077,dmask=0077 /dev/partisi boot /mnt/boot
mount –mkdir -o rw,nodev,nosuid,relatime /dev/comet/vars /mnt/var
mount –mkdir -o rw,nodev,nosuid,noexec,relatime /dev/comet/vlog /mnt/var/log
mount –mkdir -o rw,nodev,nosuid,noexec,relatime /dev/comet/vaud /mnt/var/log/audit
mount –mkdir -o rw,nodev,nosuid,noexec,relatime /dev/comet/vtmp /mnt/var/tmp
mount –mkdir -o rw,nodev,nosuid,relatime /dev/comet/home /mnt/home
mount –mkdir -o rw,nodev,nosuid,relatime /dev/comet/podman /mnt/var/lib/containers
```

## Cek Partisi
```
lsblk
```

## Instalasi sistem dasar & chroot
```
pacstrap /mnt base amd-ucode linux-lts linux-lts-headers linux-firmware mkinitcpio lvm2 git neovim firewalld openssh sudo pacman wget curl grep iwd podman
genfstab -U /mnt/etc/fstab
echo ‘“tmpfs /tmp tmpfs defaults,rw,nodev,nosuid,noexec,relatime,size=1G 0 0” >> /mnt/etc/fstab
cp /etc/systemd/network/*  /mnt/etc/systemd/network
arch-chroot /mnt
```

## Konfigurasi hostname, waktu, dan bahasa
```
echo server > /etc/hostname
```
```
ln -sf /usr/share/zoneinfo/Asia/Jakarta /etc/localtime
hwclock –systohc
```
```
nvim /etc/locale.gen
hapus hastag 
#en_US.UTF-8 UTF-8
#en_US ISO-8859-1
locale-gen
locale > /etc/locale.conf
nvim /etc/locale.conf
LANG=C.UTF-8 (LANG=en_US.UTF-8)
LC_ALL= (ditambahin en_US.UTF-8)
```

## Membuat user
```
useradd -m catchers
passwd catchers
echo “catchers ALL=(ALL:ALL) ALL” > /etc/sudoers.d/catchers
su catchers
sudo su
enter password
```

```
mkdir /etc/cmdline.d
touch /etc/cmdline.d/{01-boot.conf,02-misc.conf}
```

## Cek partisi
```
lsblk
```

```
cat /etc/cmdline.d/01-boot.conf
echo “rd.luks.name=$(blkid -s UUID -o value /dev/partisi boot)=proc root=/dev/comet/root” > /etc/cmdline.d/01-boot.conf
echo rw > /etc/cmdline.d/02-misc.conf
```

```
nvim /etc/mkinitcpio.conf
bagian HOOKS akhir tambahin (sd-encrypt lvm2)
```


```
nvim /etc/mkinitcpio.d/linux-lts.conf.preset
= mkinitcpio preset file for the 'linux-lts' package
ALL_config="/etc/mkinitepio.conf"
ALL_kver="/boot/vmlinuz-linux-Its"
ALL_kerneldest="/boot/vmlinuz-linux-lts"
PRESETS=( 'default')
#PRESETS=('default' ‘fallback')
#default_config="/etc/mkinitcpio.conf”
#default_image="/boot/initramfs-linux-lts.img”
 default_uki="/boot/EFI/Linux/arch-linux-lts.efi"
#default_options="--splash /us/share/systend/bootctl/splash-arch.bmp”
#fallback_config=”/etc/mkinitcpio.conf”
#fallback_image="/boot/initramfs-linux-lts-fallback.img “
#fallback_uki=”/efi/EFI/Linux/arch-linux-lts-fallback.efi"
#fallback_options="-S autodetect” ```
```

```
bootctl –path=/boot install
```

```
mkinitcpio -P 
```

```
systemctl enable systemd-networkd
systemctl enable systemd-resolved
systemctl enable iwd 
systemctl enable firewalld
systemctl enable sshd
```

```
exit
```

```
umount -R /mnt
```

```
reboot
```
