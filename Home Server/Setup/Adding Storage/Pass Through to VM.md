#### Resources

[docs](https://pve.proxmox.com/wiki/Passthrough_Physical_Disk_to_Virtual_Machine_(VM)
[How to: Passthrough HDD/SSD/Physical disks to VM on Proxmox VE(PVE)](https://dannyda.com/2020/08/26/how-to-passthrough-hdd-ssd-physical-disks-to-vm-on-proxmox-vepve/)
[Toricorn](https://toricorn.tech/passthrough-physical-disk-to-proxmox-vms/)
[Harveys Virtual Environment - # Passthrough Physical Disk To A Proxmox VM](https://www.youtube.com/watch?v=WgCl4zPdBzc)
[# Linux Crash Course - The /etc/fstab file](https://www.youtube.com/watch?v=A7xH74o6kY0)

1) Locate id of disk on host
```bash
ls -l /dev/disk/by-id/
```

2) Check `VM > Hardware` to see the `scsi` number (suffix)

3) Add disk to VM with scsi + 1
```bash
qm set [VMID] -scsi[number] /dev/disk/by-id/[ID]
```

4) Edit `/etc/pve/qemu-server/[VMID].conf` to add serial number
```bash
vim /etc/pve/qemu-server/101.conf
```

looks like:
```bash
scsi1: /dev/disk/by-id/ata-ST4000DM004-2U9104_ZTT5AHF7,size=3907018584K,serial=ZTT5AHF7
```

5) Check on Proxmox GUI that hard drive is available
6) Double click HDD and deselect `Backup` so that files aren't backed up when VM is, or it will be huge & take ages.
7) Log in to VM and find location of hard drive
```bash
lsblk
```

8) Create a directory in `mnt` to mount the drive
```bash
sudo mkdir /mnt/host-HDD1
```

9) FInd id of the hard drive
```bash
sudo blkid
```

10) Edit `/etc/fstab`
```bash
UUID=XXXXXXXXX-XXXXXX-XXXX-XXX-XXXXXX /mnt/host-HDD1 exts defaults 0 0 
```

11) Reload daemon
```bash
sudo systemctl daemon-reload
sudo mount -a
```

13) Check that the drive is mounted
```bash
lsblk
```

11) Give access to all users
```bash
sudo chmod -R 777 /mnt/host-HDD1
```
