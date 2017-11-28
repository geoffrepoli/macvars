## Mac System Information

###### STARTUP DISK NAME <sup>(removed in 10.13)</sup>
```bash
ioreg -rd1 -c CoreStorageGroup | awk -F\" '/lvg.n/{print $(NF-1)}'
```

###### SERIAL NUMBER
```bash
ioreg -rd1 -c IOPlatformExpertDevice | awk -F\" '/S.*N/{print $(NF-1)}'
```

###### HARDWARE MODEL
```bash
sysctl -n hw.model
```

###### MARKETING MODEL
<sup>(credit: [@WardsParadox](https://github.com/WardsParadox))</sup>
```bash
/usr/libexec/PlistBuddy -c "Print :$(sysctl -n hw.model):_LOCALIZABLE_:marketingModel" /System/Library/PrivateFrameworks/ServerInformation.framework/Resources/English.lproj/SIMachineAttributes.plist
```

###### EFI VERSION
```bash
/usr/libexec/efiupdater | awk '/Raw/{print $NF}'
```

###### HARDWARE UUID/UDID
```bash
ioreg -rd1 -c IOPlatformExpertDevice | awk -F\" '/UUID/{print $(NF-1)}'
```

###### LOGICAL VOLUME UUID <sup>(removed in 10.13)</sup>
```bash
ioreg -rd1 -c CoreStorageLogical | awk -F\" '/"UUID"/{print $(NF-1)}'
```

###### LOGICAL VOLUME GROUP UUID <sup>(removed in 10.13)</sup>
```bash
ioreg -rd1 -c CoreStorageLogical | awk -F\" '/LVG/{print $(NF-1)}'
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

###### LAST REBOOT
```bash
sysctl -n kern.boottime | awk -F'} ' '{print $NF}' | xargs -I{} date -jf "%a %b %d %T %Y" {} "+%F %T %Z"
```

###### USER IDLE TIME
```bash
ioreg -rd1 -c IOHIDSystem | awk '/HIDIdleTime/{printf "%1.0f\n",$NF/1000000000}'
# use in a while loop: `while (( $(ioreg -rd1 -c IOHIDSystem | awk '/HIDIdleTime/{printf "%1.0f\n",$NF/1000000000}') < [time in seconds] )); do sleep 0.1; done`
```

###### BATTERY CYCLE COUNT
```bash
ioreg -rd1 -c AppleSmartBattery | awk '/"CycleCount"/{print $NF}'
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
