## Mac Network Information

###### ACTIVE NETWORK INTERFACE
```bash
/usr/sbin/scutil --nwi | grep -A1 "IPv4 network" | sed '1d' | awk '{print $1}'
```

###### ACTIVE NETWORK SERVICE
```bash
/usr/sbin/networksetup -listallhardwareports | grep $(/usr/sbin/scutil --nwi | grep -A1 "IPv4 network" | sed '1d' | awk '{print $1}') -B1 | awk -F': ' '/Hardware Port/{print $NF}'
```

###### ACTIVE MAC ADDRESS
```bash
/usr/sbin/networksetup -getmacaddress $(/usr/sbin/scutil --nwi | grep -A1 "IPv4 network" | sed '1d' | awk '{print $1}') | awk '{print $3}'
```

###### WI-FI INTERFACE
```bash
/usr/sbin/networksetup -listallhardwareports | grep -A1 Wi-Fi | awk -F': ' '/Device/{print $NF}'
```

###### WI-FI POWER
```bash
/usr/sbin/networksetup -getairportpower "$(/usr/sbin/networksetup -listallhardwareports | grep -A1 Wi-Fi | awk -F': ' '/Device/{print $NF}')" | awk '{print $NF}'
```

###### CURRENT SSID
```bash
/usr/sbin/networksetup -getairportnetwork "$(/usr/sbin/networksetup -listallhardwareports | grep -A1 Wi-Fi | awk -F': ' '/Device/{print $2}')" 2> /dev/null | awk -F': ' '{print $NF}'
```

###### IP ADDRESS
```bash
/usr/sbin/ipconfig getifaddr "$(/usr/sbin/scutil --nwi | grep -A1 "IPv4 network" | sed '1d' | awk '{print $1}')"
```
