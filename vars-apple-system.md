## System Information

###### STARTUP DISK NAME
```bash
/usr/sbin/ioreg -c CoreStorageGroup -d 16 | awk -F\" '/com.apple.corestorage.lvg.name/{print $(NF-1)}'
```

###### SERIAL NUMBER
```bash
/usr/sbin/ioreg -c IOPlatformExpertDevice -d 2 | awk -F\" '/IOPlatformSerialNumber/{print $(NF-1)}'
```

###### HARDWARE MODEL
```bash
/usr/sbin/sysctl -n hw.model
```

###### COMPUTER NAME ("FRIENDLY NAME")
```bash
/usr/sbin/scutil --get ComputerName
```

###### BONJOUR NAME ("LOCAL SUBNET NAME")
```bash
/usr/sbin/scutil --get LocalHostName
```
###### CERTIFICATE EXPIRATION DATE
```bash
/usr/bin/security find-certificate -c <NAME_OF_CERT> -p | /usr/bin/openssl x509 -enddate -noout | cut -d\= -f2 | xargs -I {} date -jf "%b %d %T %Y %Z" {} "+%F %T %Z"
```
###### HOSTNAME
```bash
/usr/sbin/sysctl -n kern.hostname
# note: can simply use environment variable $HOSTNAME
```

###### RAM (GB)
```bash
expr $(/usr/sbin/sysctl -n hw.memsize) / 1073741274
# set variable to above with your_variable=$(( $(/usr/sbin/sysctl -n hw.memsize) / 1073741274 ))
```

###### GATEKEEPER STATUS
```bash
/usr/sbin/spctl --status | awk '{print toupper(substr($NF,1,1)) substr($NF,2)}'
```

###### SPOTLIGHT INDEXING STATUS
```bash
/usr/bin/mdutil --status / | sed -e '1d' -e 's/\.//' | awk '{print toupper(substr($NF,1,1)) substr($NF,2)}'
```

###### TIME ZONE
```bash
systemsetup -gettimezone | awk -F': ' '{print $NF}'
```

###### NETWORK TIME STATUS
```bash
/usr/sbin/systemsetup -getusingnetworktime | awk -F': ' '{print $NF}'
```

###### NETWORK TIME SERVER
```bash
/usr/sbin/systemsetup -getnetworktimeserver | awk -F': ' '{print $NF}'
```

###### SSH STATUS
```bash
/usr/sbin/systemsetup -getremotelogin | awk -F': ' '{print $NF}'
```

###### PRINTER SHARING
```bash
/usr/sbin/cupsctl | grep share | tail -c2
```

###### COMPUTER SLEEP
```bash
/usr/sbin/systemsetup -getcomputersleep | awk -F': ' '{print $NF}' | sed 's/after\ //'
```

###### DISPLAY SLEEP
```bash
/usr/sbin/systemsetup -getdisplaysleep | awk -F': ' '{print $NF}' | sed 's/after\ //'
```

###### HARD DISK SLEEP
```bash
/usr/sbin/systemsetup -getharddisksleep | awk -F': ' '{print $NF}' | sed 's/after\ //'
```
