# Instalasii Os Server
1. Melihat / Cek Partisi

   lsblk
   ```
2. Enskripsi Partisi (LUKS)
   cryptsetup luksFormat /dev/nvme0n1p6
# Ketik YES (kapital) untuk konfirmasi, lalu masukkan passphrase (Password)

cryptsetup luksOpen /dev/nvme0n1p6 proc
# Buka partisi terenkripsi dengan nama mapper "proc"
```
3. Setup LVM


