pacman -S linux-hardened linux-hardened-headers

nvim /etc/fstab
nvim /etc/mkinitcpio.d/linux
nvim /etc/mkinitcpio.d/linux-lts.preset
nvim /etc/mkinitcpio.d/linux-hardened.preset
nvim /etc/mkinitcpio.d/linux-hardened.preset
mkinitcpio -P
ls /boot/efi/Linux/arch-linux-hardened.efi
ls /boot/efi/Linux arch-linux-lts.efi
nvim /etc/mkinitcpio.d/linux-hardened.preset
nvim /etc/mkinitcpio.d/linux-hardened.preset
ls /boot/efi/Linux/arch-linux-hardened.efi
mkinitcpio -P
ls /boot/efi/Linux/arch-linux-hardened.efi /boot/efi/Linux/arch-linux-hardened.efi
exit
