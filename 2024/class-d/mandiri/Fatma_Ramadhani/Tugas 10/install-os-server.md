# Dokumentasi Penginstalan OS Linux untuk Server
## Nama: Fatma Ramadhani
## NIM: 12402051050157
## Mata Kuliah: Perpustakaan dan Arsip Digital
## Dosen Pengampu: Al Muhdil Karim, S. IP., M.Hum
---
## Masuk ke Blackbird Amanda
## Hubungkan ke jaringan internet terlebih dahulu
```
iwctl
```
## Mulai rec Asciinema
```
asciinema rec (nama file).cast
```
## Check partisi yang ada
```
lsblk
```
## Lakukan Crypsetup dan format luks
```
cryptsetup luksFormat /dev/partisi_root
```
lalu, jangan lupa masukin passwd yaaa
## Lanjut kita buka partisi luks
```
crypsetup luksOpen /dev/(partisi_root) (nama_device)
```
## Lanjut kita buat physical volume nya
```
pvcreate /dev/mapper/(nama_device)
```
## Selanjutnya kita buat volume grup
```
vgcreate nama_grup /dev/mapper/(nama_device)
```
## Habis ituuu, kita buat logical volume nya
```
lvcreate -L 10G (nama_grup) -n root
```
```
lvcreate -L 10G (nama_grup) -n vars
```
```
lvcreate -L 1G (nama_grup) -n vlog
```
```
lvcreate -L 1G (nama_grup) -n vtmp
```
```
lvcreate -L 1G (nama_grup) -n vaud
```
```
lvcreate -L 10G (nama_grup) -n home
```
```
lvcreate -l100%FREE (nama_grup) -n podman
```
## Lanjut, kita format Partisi
```
mkfs.vfat -F32 -n BOOT /dev/partisi_boot
```
```
mkfs.ext4 /dev/nama_grup/root
```
```
mkfs.ext4 /dev/nama_grup/vars
```
```
mkfs.ext4 /dev/nama_grup/vtmp
```
```
mkfs.ext4 /dev/nama_grup/vaud
```
```
mkfs.ext4 /dev/nama_grup/vlog
```
```
mkfs.ext4 /dev/nama_grup/home
```
```
mkfs.ext4 /dev/nama_grup/podman
```
## Selanjutnya kita periksa kembali yaaa
```
lsblk
```
kalau sudah, kita lanjut ke step berikutnya yaa
## Langkah selanjutnya, kita mounting
