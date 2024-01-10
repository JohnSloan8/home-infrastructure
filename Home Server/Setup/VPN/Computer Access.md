
##### On Computer 
1) Install Wireguard

##### On Container
1) Generate new client
```bash
pivpn -a
```
2) Enter name for client
3) Copy content of config file 
```bash
cat /home/john/configs/[client-name].conf
```

##### On Computer
1) Create file with contents of the config file above
2) Import on Wireguard GUI