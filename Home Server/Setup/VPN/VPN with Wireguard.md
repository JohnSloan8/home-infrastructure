##### Resources 

YouTube: Homelab Tim - [Easiest VPN on Proxmox with WireGuard](https://www.youtube.com/watch?v=V9sWhnYQvpE)
[PiVPN](https://www.pivpn.io/)


##### Add OS Template
1) In `local > CT Templates` select `templates`
2) Download Debian 12
##### Create Container
1) Select `Create CT`
2) All defaults except for enabling DCHP
##### Expose Container on Host Machine

1) Log into host machine
```bash
cd /etc/pve/lxc
vim [container number].conf
```

2) Add the following lines to the bottom of the file (below `unpriviliged: 1`)
```bash
lxc.cgroup2.devices.allow: c 10:200 rwm
lxc.mount.entry: /dev/net dev/net none bind,create=dir
```

3) Run the following command
```bash
chown 100000:100000 /dev/net/tun
```

4) Check that it worked
```bash
ls -l /dev/net/tun
```

Output should be something like this

```bash
crw-rw-rw- 1 100000 100000 10, 200 Dec 22 13:26 /dev/net/tun
```

##### Prepare Container

1) Start container on Proxmox & log in as root

```bash
apt upgrade && apt update -y
apt install curl -y
```

2) Use curl command for PiVPN
```bash
curl -L https://install.pivpn.io | bash
```

3) Follow Installer  (`109.255.185.32` is the public IP address)

4) Reboot when done