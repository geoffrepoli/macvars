## Mac System Information

###### STARTUP DISK NAME
```bash
ioreg -rc CoreStorageGroup | awk -F\" '/lvg.name/{print $(NF-1)}'
```

###### SERIAL NUMBER
```bash
ioreg -rc IOPlatformExpertDevice -d2 | awk -F\" '/SerialNumber/{print $(NF-1)}'
```

###### HARDWARE UUID/UDID
```bash
ioreg -c IOPlatformExpertDevice -d 2 | awk -F\" '/IOPlatformUUID/{print $(NF-1)}'
```

###### HARDWARE MODEL
```bash
sysctl -n hw.model
```

###### LOGICAL VOLUME UUID
```bash
ioreg -rc CoreStorageLogical | awk -F\" '/"UUID"/{print $(NF-1)}'
```

###### LOGICAL VOLUME GROUP UUID
```bash
ioreg -rc CoreStorageLogical | awk -F\" '/LVG/{print $(NF-1)}'
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
security find-certificate -c <NAME_OF_CERT> -p | /usr/bin/openssl x509 -enddate -noout | cut -d= -f2 | xargs -I{} date -jf "%b %d %T %Y %Z" {} "+%F %T %Z"
```

###### RAM (GB)
```bash
sysctl -n hw.memsize | awk '{print $0/1073741274}'
```

###### USER IDLE TIME
```bash
ioreg -rc IOHIDSystem | awk '/HIDIdleTime/{printf "%1.0f\n",$NF/1000000000}'
# use in a while loop: `while true; do ioreg -rc IOHIDSystem | awk '/HIDIdleTime/{printf "%1.0f\n",$NF/1000000000}'; done`
```

###### BATTERY CYCLE COUNT
```bash
ioreg -rc AppleSmartBattery | awk '/"CycleCount"/{print $NF}'
```

###### GATEKEEPER STATUS
```bash
spctl --status | awk '{print toupper(substr($NF,1,1))substr($NF,2)}'
```

###### SYSTEM INTEGRITY PROTECTION STATUS
```bash
csrutil status | awk -F: '{gsub(/\./,"");print toupper(substr($NF,2,1)) substr($NF,3)}'
```

###### SPOTLIGHT INDEXING STATUS
```bash
mdutil --status / | awk 'END{gsub(/\./,"");print toupper(substr($NF,1,1))substr($NF,2)}'
```

###### TIME ZONE
```bash
systemsetup -gettimezone | awk -F: '{print substr($NF,2)}'
```

###### NETWORK TIME STATUS
```bash
systemsetup -getusingnetworktime | awk -F: '{print substr($NF,2)}'
```

###### NETWORK TIME SERVER
```bash
systemsetup -getnetworktimeserver | awk -F: '{print substr($NF,2)}'
```

###### SSH STATUS
```bash
systemsetup -getremotelogin | awk -F: '{print substr($NF,2)}'
```

###### PRINTER SHARING
```bash
cupsctl | awk -F= '/share/{print $2}'
```

###### COMPUTER SLEEP (SECONDS)
```bash
systemsetup -getcomputersleep | awk -F: '{print substr($2,2)}'
```

###### DISPLAY SLEEP (SECONDS)
```bash
systemsetup -getdisplaysleep | awk -F: '{gsub(/[A-Za-z]/,"");print $2*60}'
```

###### HARD DISK SLEEP (SECONDS)
```bash
systemsetup -getharddisksleep | awk -F: '{gsub(/[A-Za-z]/,"");print $2*60}'
```

###### LIST ALL SIP-PROTECTED FILES
```bash
find -x / /System/Library/* -flags restricted -prune -print
# Apple does not regularly maintain /System/Librarty/Sandbox/rootless.conf, so this will print every file/directory that is protected by System Integrity Protection
```
