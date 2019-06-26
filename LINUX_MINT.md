# LINUX MINT
#### Dead freezes
Add the following line to either `/etc/sysctl.conf`  

```bash
fs.inotify.max_user_watches = 524288
```

Then run  
```bash
sudo sysctl -p --system
```
#### LSB_RELEASE
If some script use `lsb_release -sc` command  
First you need execute:
```bash
export LSB_ETC_LSB_RELEASE=/etc/upstream-release/lsb-release
```