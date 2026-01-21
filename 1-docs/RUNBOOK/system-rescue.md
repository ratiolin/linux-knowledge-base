# System Rescue Runbook

## Entry Points
- Cloud provider console (root access)
- Recovery / rescue mode if system fails to boot

## Mount & Chroot
```bash
mount /dev/vda1 /mnt
mount --bind /dev /mnt/dev
mount --bind /proc /mnt/proc
mount --bind /sys /mnt/sys
chroot /mnt
```
## Common Repairs

### sudoers broken
```
visudo
```
### sshd fails
```
systemctl status sshd
systemctl reload sshd
```
### fstab misconfiguration
```
vi /etc/fstab
mount -a
```
### Verification
```
ssh login works

sudo -l works

systemctl status critical services
```