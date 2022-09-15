## Mac System Information

#### DEVICE INFO

###### SERIAL NUMBER
```bash
ioreg -rd1 -c IOPlatformExpertDevice | awk -F\" '/S.*N/{print $(NF-1)}'
```

###### HARDWARE MODEL
```bash
sysctl -n hw.model
```

###### MARKETING MODEL
<sub>APPLE SILICON</sub>
```bash
ioreg -rk product-name | awk -F\" '/product-name/{print $(NF-1)}'
```

<sub>INTEL</sub>
```bash
/usr/libexec/PlistBuddy -c "Print :$(sysctl -n hw.model):_LOCALIZABLE_:marketingModel" /System/Library/PrivateFrameworks/ServerInformation.framework/Versions/A/Resources/en.lproj/SIMachineAttributes.plist
```

###### HARDWARE UUID/UDID
```bash
ioreg -rd1 -c IOPlatformExpertDevice | awk -F\" '/UUID/{print $(NF-1)}'
```

###### COMPUTER NAME ("FRIENDLY NAME")
```bash
scutil --get ComputerName
```

###### BONJOUR NAME ("LOCAL SUBNET NAME")
```bash
scutil --get LocalHostName
```

###### EFI VERSION (T2 INTEL MACS)
```bash
/usr/libexec/efiupdater | awk '/string/{print $NF}'
```

### COMPUTER STATE

###### LAST REBOOT
```bash
sysctl -n kern.boottime | awk -F'} ' '{print $NF}' | xargs -I{} date -jf "%a %b %d %T %Y" {} "+%F %T %Z"
```

###### BATTERY CYCLE COUNT
```bash
ioreg -rd1 -c AppleSmartBattery | awk '$1=="\"CycleCount\""{print $NF}'
```

###### SPOTLIGHT INDEXING STATUS
```bash
mdutil --status / | awk 'END{gsub(/\./,"");print toupper(substr($NF,1,1))substr($NF,2)}'
```

###### COMPUTER SLEEP IN SECONDS
```bash
systemsetup -getcomputersleep | awk -F: '{print substr($2,2)}'
```

###### DISPLAY SLEEP IN SECONDS
```bash
systemsetup -getdisplaysleep | awk -F: '{gsub(/[A-Za-z]/,"");print $2*60}'
```

###### HARD DISK SLEEP IN SECONDS
```bash
systemsetup -getharddisksleep | awk -F: '{gsub(/[A-Za-z]/,"");print $2*60}'
```

###### PRINTER SHARING
```bash
cupsctl | awk -F= '/share/{print $2}'
```

### SECURITY

###### GATEKEEPER STATUS
```bash
spctl --status | awk '{print toupper(substr($NF,1,1))substr($NF,2)}'
```

###### SYSTEM INTEGRITY PROTECTION STATUS
```bash
csrutil status | awk -F: '{gsub(/\./,"");print toupper(substr($NF,2,1)) substr($NF,3)}'
```

###### CERTIFICATE EXPIRATION DATE
```bash
security find-certificate -c <NAME_OF_CERT> -p | /usr/bin/openssl x509 -enddate -noout | cut -d= -f2 | xargs -I{} date -jf "%b %d %T %Y %Z" {} "+%F %T %Z"
```

###### SSH STATUS
```bash
systemsetup -getremotelogin | awk -F: '{print substr($NF,2)}'
```

###### LIST ALL SIP-PROTECTED FILES
```bash
find -x / /System/Library/* -flags restricted -prune -print 2>/dev/null
# Apple does not regularly maintain /System/Librarty/Sandbox/rootless.conf, so this will print every file/directory that is protected by System Integrity Protection. This is mostly for if you're curious as this will take a long time to run & will dump a lot of output
```

### TIME

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

### STORAGE & MEMORY

###### STARTUP DISK NAME (HFS)
```bash
ioreg -rd1 -c CoreStorageGroup | awk -F\" '/lvg.n/{print $(NF-1)}'
```

###### LOGICAL VOLUME UUID (HFS)
```bash
ioreg -rd1 -c CoreStorageLogical | awk -F\" '/"UUID"/{print $(NF-1)}'
```

###### LOGICAL VOLUME GROUP UUID (HFS)
```bash
ioreg -rd1 -c CoreStorageLogical | awk -F\" '/LVG/{print $(NF-1)}'
```

###### RAM (GB)
```bash
sysctl -n hw.memsize | awk '{print $0/1073741274}'
```
