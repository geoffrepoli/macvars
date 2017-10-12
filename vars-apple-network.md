## Mac Network Information

###### ACTIVE NETWORK INTERFACE (e.g., en0)
```bash
scutil --nwi | awk '/^IPv4/{i[NR+1]};NR in i{print $1}'
```

###### ACTIVE NETWORK SERVICE (e.g., Wi-Fi)
```bash
networksetup -listallhardwareports | awk -F': ' -v v="$(scutil --nwi | awk '/^IPv4/{i[NR+1]};NR in i{print $1}')" '$0~v{print a}{a=$NF}'
```

###### ACTIVE MAC ADDRESS
```bash
networksetup -getmacaddress $(scutil --nwi | awk '/IPv4/{getline;print $1;exit}') | awk '{print $3}'
```

###### WI-FI INTERFACE
```bash
networksetup -listallhardwareports | awk '/Wi-Fi/{getline;print $2}'
```

###### WI-FI POWER
```bash
networksetup -getairportpower $(networksetup -listallhardwareports | awk -F': ' '/Wi-Fi/{getline;print $2}') | awk '{print $NF}'
```

###### CURRENT SSID
```bash
networksetup -getairportnetwork $(networksetup -listallhardwareports | awk -F': ' '/Wi-Fi/{getline;print $2}') 2>/dev/null | awk -F': ' '{print $NF}'
```

###### INTERNAL IP ADDRESS
```bash
scutil --nwi | awk '/^IPv4/{i[NR+2]};NR in i{print $3;exit}'
```

###### PUBLIC IPv4 ADDRESS
```bash
dig +short myip.opendns.com @resolver1.opendns.com
```

###### IPV6 ADDRESS
```bash
scutil --nwi | awk '/^IPv6/{i[NR+2]};NR in i{print $3}'
```
