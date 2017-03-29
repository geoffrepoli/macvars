### System Information

###### STARTUP DISK NAME
```bash
ioreg -l -c IODeviceTree | awk -F\" '/com.apple.corestorage.lvg.name/{print $(NF-1)}'
```

###### SERIAL NUMBER
```bash
ioreg -c IOPlatformExpertDevice -d 2 | awk -F\" '/IOPlatformSerialNumber/{print $(NF-1)}'
```

###### HARDWARE MODEL
```bash
sysctl -n hw.model
```

###### COMPUTER NAME ("FRIENDLY NAME")
```bash
scutil --get ComputerName
```

###### BONJOUR NAME ("LOCAL SUBNET NAME")
```bash
scutil --get LocalHostName
```

###### HOSTNAME *(note: can simply use environment variable `$HOSTNAME`)*
```bash
sysctl -n kern.hostname
```

###### RAM (GB)
```bash
expr $(( $(sysctl -n hw.memsize) / 1073741274 ))
```

###### GATEKEEPER STATUS
```bash
spctl --status | awk '{print toupper(substr($NF,1,1)) substr($NF,2)}'
```

###### SPOTLIGHT INDEXING STATUS
```bash
mdutil --status / | sed -e '1d' -e 's/\.//' | awk '{print toupper(substr($NF,1,1)) substr($NF,2)}'
```

###### TIME ZONE
```bash
systemsetup -gettimezone | awk '{print $NF}'
```

###### NETWORK TIME STATUS
```bash
systemsetup -getusingnetworktime | awk '{print $NF}'
```

###### NETWORK TIME SERVER
```bash
systemsetup -getnetworktimeserver | awk '{print $NF}'
```

###### SSH STATUS
```bash
systemsetup -getremotelogin | awk '{print $NF}'
```

###### PRINTER SHARING
```bash
cupsctl | grep share | tail -c2
```

###### COMPUTER SLEEP
```bash
systemsetup -getcomputersleep | awk -F': ' '{print $NF}' | sed 's/after\ //'
```

###### DISPLAY SLEEP
```bash
systemsetup -getdisplaysleep | awk -F': ' '{print $NF}' | sed 's/after\ //'
```

###### HARD DISK SLEEP
```bash
systemsetup -getharddisksleep | awk -F': ' '{print $NF}' | sed 's/after\ //'
```
