# Pertemuan 5 & 6: Installasi Arch LInux dan KDE Plasma #
### Nama: Amelia Salsabila Santoso ###
### NIM: 12402051030089 ###
### Kelas: 4D ###

## Persiapan Sebelum Installasi ##
- Unduh File ISO Arch LInux dari situs resmi
- Unduh Rufus dan siapkan flashdisk, sambungkan ke flashdisk dan gunakan rufus untuk membuat USB Flasdisk biasa menjadi bootable media Installer

<img width="1280" height="960" alt="photo_6100275688876217426_y" src="https://github.com/user-attachments/assets/64d3e745-5b4b-43f4-9f29-f341a5afc02a" />
<img width="1280" height="960" alt="photo_6100275688876217427_y" src="https://github.com/user-attachments/assets/c8148052-5df3-4a76-a15d-bf8e600433a1" />
<img width="960" height="1280" alt="photo_6100275688876217429_y" src="https://github.com/user-attachments/assets/179f18e1-15a7-48c3-ab6f-dfb787bb5f77" />
lakukan juga shrink di disk management untuk memberikan ruang kosong untuk linux
<img width="1280" height="960" alt="photo_6100275688876217438_y" src="https://github.com/user-attachments/assets/58283b59-2e48-48ac-9e18-fb9b61998246" />

## Proses Installasi ##
Restart Kemudian Spam Del (tergantung laptop biasanya f2), kemudian akan masuk ke bios, magikan security boot, save changes kemudian pilih USB yang akan dibuat Penginstallan archlinux kemudian layar akan mati dan akan memiliki tampilan seperti ini 
<img width="1280" height="960" alt="1000052153" src="https://github.com/user-attachments/assets/26663441-52a1-41a0-845f-3624976a77f9" />

perintah awal di live environment ketik cat /sys/firmware/efi/fw_platform_size

Menghubungkan ke internet
- Ketik iwctl
- Ketik device list (untuk ngecek driver wifi setiap laptop)
- station wlan0 scan (untuk memindai jaringan yang ada)
- station wlan0 get-networks (untuk menghubungkan ke jaringan yang sudah ditentukan)
- station wlan0 connect nama-wifi
- masukkan password 
- exit
- Ketik ping 1.1.1.1 (untuk cek apakah jaringan sudah konek)
<img width="1280" height="960" alt="1000052154" src="https://github.com/user-attachments/assets/903f2cda-3b3d-4d20-86a4-ede01f413be7" />

Checking partisi
- ketik lsblk -o name,fstype,size (untuk melihat partisi)
Kemudian bagi partisi dan format partisi
<img width="1280" height="960" alt="1000052155" src="https://github.com/user-attachments/assets/57495b89-0932-4533-95c3-0497de880320" />
<img width="1280" height="960" alt="1000052157" src="https://github.com/user-attachments/assets/c3095363-d964-40f0-8274-8ed63c366309" />
<img width="1280" height="960" alt="1000052165" src="https://github.com/user-attachments/assets/c6712d52-019f-466c-b87d-0227795a65e2" />
<img width="1280" height="960" alt="1000052156" src="https://github.com/user-attachments/assets/c3518649-2378-4cf3-a997-61ac1247950b" />
<img width="1280" height="960" alt="1000052160" src="https://github.com/user-attachments/assets/7088e389-a698-4bd2-8730-8f95501cc33a" />



Instalasi sistem dasar
- Ketik pacstrap -K /mnt base base-devel linux linux-firmware neovim git networkmanager

Membuat fstab (untuk menetukan partisi mana yang otomatis dimount saat boot)
genfstab -U /mnt >> /mnt/etc/fstab

trs masuk sistem arch-chroot /mnt
buat mengubah root install menjadi arch yang baru dipasang 

Download pengelola jaringan
sudo pacman -S iwd dhcpcd
Setelah itu ketik Y dipertanyaan
Baru terinstall

Lalu buka service nya
systemctl enable iwd.service
systemctl enable dhcpcd.service

Mengatur Timezone
Untuk mengsinkronasi waktu di Indonesia 
ln -sf /usr/share/zoneinfo/Asia/Jakarta /etc/localtime
lalu sinkronin : hwclock --systohc

Localization 
Cek nvim
Cara keluar (:q) enter
locale-gen

isi /etc/locale.conf:
echo "LANG=en_US.UTF-8" > /etc/locale.conf

Cara cek file nya
cat /etc/locale.cont

Buat Hostname
echo "Nova" > /etc/hostname
ini nama komputer

Generate initramfs
Membuat image boot awal linux
mkinitcpio -P

Password Root
passwd….

Menambahkan user
useradd -m amelia [perkondisian]
passwd nuraini
echo nuraini 'ALL=(ALL:ALL) ALL' >> /etc/sudoers.d/none
Itu untuk shortcut nambahin cammand file

Install boatloader 
instalasi grub
pacman -S grub efibootmgr
grub-install --target=x86_64-efi --efi-directory=boot --bootloader-id=GRUB
grub-mkconfig -o /boot/grub/grub.cfg

Install 

REBOOT
exit
unmount
umount -R /mnt

reboot
Setelah laptop mati cabut flashdisk 

