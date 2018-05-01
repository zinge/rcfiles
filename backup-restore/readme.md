# Helper
```
lsblk -- show disk device blocks

sudo blkid -- show part id`s
```

# Backup files in fs
```
tar -cvpzf backup.tar.gz --exclude=/backup.tar.gz --one-file-system /
```
## If dont full backup without tar archive you can only copy files
```
sudo rsync -aXS --exclude='/*/.gvfs' /home/. /media/home/.
```

# If use EFI backup too
```
EFI in /boot/efi
```

# Restore
```
sudo tar -xvpzf /path/to/backup.tar.gz -C / --numeric-owner
```
# Correct fstab

# Mount
```
for f in dev dev/pts proc sys ; do mount --bind /$f /media/newroot/$f ; done
```
# Chroot
```
chroot /media/newroot
```

# Grub
```
grub-install /dev/sdX
grub-install --recheck /dev/sdX
update-grub
```

# Umount
```
exit
for f in dev dev/pts proc sys ; do umount /media/newroot/$f ; done
```
