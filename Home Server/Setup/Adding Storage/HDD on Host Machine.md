#### Resources

[virtualize everything](https://www.youtube.com/@virtualizeeverything) - [How to Add a Storage Drive to Proxmox 7 using the Web Interface](https://jellyfin.org/docs/general/installation/linux)
##### Prepare Hard Drive
1) Go to `node > Disks` and find the hard drive. It should have `Usage` set to `No`
2) Click `Wipe Disk`
3) Click `Initialise Disk with GPT`.  (GPT is a partition table format)
4) Click `directory > Create Directory`
5) Choose ext4 (or xfs) and name the drive
