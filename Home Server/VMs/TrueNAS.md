l#### Resources

[How to Install TrueNAS in Proxmox with HDD Passthrough!](https://www.youtube.com/watch?v=MkK-9_-2oko)

##### Prepare TrueNAS ISO
1) Download [TrueNAS Core](https://www.truenas.com/truenas-core/)
2) Go to `local storage > ISO Images` on Proxmox
3) Click `upload` and the `select file` 

##### Setup VM
1) Create new VM
2) Give it 2 cores and 8GB RAM (8192)
3) [[Pass Through to VM|Mount hard drive]] (use lshw for serial number of drive - in video). Only do steps on host.

##### Start VM
1) Follow steps in video