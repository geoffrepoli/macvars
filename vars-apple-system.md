## Mac System Information

###### STARTUP DISK NAME
```bash
ioreg -c CoreStorageGroup -d 16 | awk -F\" '/com.apple.corestorage.lvg.name/{print $(NF-1)}'
```

##### LOGICAL VOLUME UUID (LVUUID)
```bash
ioreg -c CoreStorageLogical | awk -F\" '/"UUID"/{print $(NF-1)}'
```

###### SERIAL NUMBER
```bash
ioreg -c IOPlatformExpertDevice -d 2 | awk -F\" '/IOPlatformSerialNumber/{print $(NF-1)}'
```

###### HARDWARE MODEL
```bash
sysctl -n hw.model
```

###### BATTERY CYCLE COUNT
```bash
ioreg -r -c AppleSmartBattery | awk '/"CycleCount"/{print $NF}'
```

###### COMPUTER NAME ("FRIENDLY NAME")
```bash
scutil --get ComputerName
```

###### BONJOUR NAME ("LOCAL SUBNET NAME")
```bash
scutil --get LocalHostName
```
###### CERTIFICATE EXPIRATION DATE
```bash
security find-certificate -c <NAME_OF_CERT> -p | /usr/bin/openssl x509 -enddate -noout | cut -d\= -f2 | xargs -I {} date -jf "%b %d %T %Y %Z" {} "+%F %T %Z"
```
###### HOSTNAME
```bash
sysctl -n kern.hostname
# note: can simply use environment variable $HOSTNAME
```

###### RAM (GB)
```bash
expr $(sysctl -n hw.memsize) / 1073741274
# set variable to above with your_variable=$(( $(/usr/sbin/sysctl -n hw.memsize) / 1073741274 ))
```

###### GATEKEEPER STATUS
```bash
spctl --status | awk '{print toupper(substr($NF,1,1)) substr($NF,2)}'
```

###### SPOTLIGHT INDEXING STATUS
```bash
mdutil --status / | awk 'END{gsub(/\./,"");print toupper(substr($NF,1,1)) substr($NF,2)}'
```

###### TIME ZONE
```bash
systemsetup -gettimezone | awk -F': ' '{print $NF}'
```

###### NETWORK TIME STATUS
```bash
systemsetup -getusingnetworktime | awk -F': ' '{print $NF}'
```

###### NETWORK TIME SERVER
```bash
systemsetup -getnetworktimeserver | awk -F': ' '{print $NF}'
```

###### SSH STATUS
```bash
systemsetup -getremotelogin | awk -F': ' '{print $NF}'
```

###### PRINTER SHARING
```bash
cupsctl | awk -F= '/share/{print $2}'
```

###### COMPUTER SLEEP
```bash
systemsetup -getcomputersleep | awk -F': ' '{print $NF}'
```

###### DISPLAY SLEEP
```bash
systemsetup -getdisplaysleep | awk -F': ' '{print $NF}'
```

###### HARD DISK SLEEP
```bash
systemsetup -getharddisksleep | awk -F': ' '{print $NF}'
```
