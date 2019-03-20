# Helped commands
- get disk information, device blocks: `lsblk`
- get partitions id's: `sudo blkid`

# Backup files by fs

## one way: fully backup fs with tar arhive and when need extract this
```
tar -cvpzf backup.tar.gz --exclude=/backup.tar.gz --one-file-system /
```
!!! ATTENTION !!!
If you use EFI type loader, need backup this(only full backup way). EFI located in `/boot/efi`

## different other: else if you plain only copy files, without full backup
```
sudo rsync -avhXS --progress --exclude='/*/.gvfs' /home/. /media/home/.
```

# Restore(if of course full backup)
```
sudo tar -xvpzf /path/to/backup.tar.gz -C / --numeric-owner
```
# Fix fstab
This question assume you understand what need. First get partition ID's. Open `/etc/fsbab` file. Check partitions ID's, fix if ID's incorrect or new. For edit `fstab` use any text editor. Best of best - `vim` ;-)

# LiveCD
If you go restore `full backup` way, or after crash partitions and need restore. Use any loved linux LiveCD image. Burn on CD or USB. Boot in resquie mode, or different mode where available console. Create partitions, restore backups(full in this instuction). Fix fstab. And get next steps for restore loader ...

## Mount
for correct restore partitions need mount first youself and dont lost next too
```
for f in dev dev/pts proc sys ; do mount --bind /$f /media/newroot/$f ; done
```

## Chroot
chroot after mounted
```
chroot /media/newroot
```

## Grub
and install boot loader, i am use `grub`
```
grub-install /dev/sdX
grub-install --recheck /dev/sdX
update-grub
```

## Umount
after boot loader installed, fstab fixed, and true check files in partitions, need exit in chroot and umount all previously mounted partitions
```
exit
for f in dev dev/pts proc sys ; do umount /media/newroot/$f ; done
```
