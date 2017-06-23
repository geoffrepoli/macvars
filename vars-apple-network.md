## Mac Network Information

###### ACTIVE NETWORK DEVICE (e.g., en0)
```bash
scutil --nwi | scutil --nwi | awk '/IPv4/{getline;print $1;exit}'
```

###### ACTIVE NETWORK SERVICE (e.g., Wi-Fi)
```bash
networksetup -listallhardwareports | grep $(scutil --nwi | scutil --nwi | awk '/IPv4/{getline;print $1;exit}') -B1 | awk -F': ' '/Hardware Port/{print $NF}'
```

###### ACTIVE MAC ADDRESS
```bash
networksetup -getmacaddress $(scutil --nwi | scutil --nwi | awk '/IPv4/{getline;print $1;exit}') | awk '{print $3}'
```

###### WI-FI DEVICE
```bash
networksetup -listallhardwareports | grep -A1 Wi-Fi | awk -F': ' '/Device/{print $NF}'
```

###### WI-FI POWER
```bash
networksetup -getairportpower "$(networksetup -listallhardwareports | grep -A1 Wi-Fi | awk -F': ' '/Device/{print $NF}')" | awk '{print $NF}'
```

###### CURRENT SSID
```bash
networksetup -getairportnetwork "$(networksetup -listallhardwareports | grep -A1 Wi-Fi | awk -F': ' '/Device/{print $2}')" 2> /dev/null | awk -F': ' '{print $NF}'
```

###### IP ADDRESS
```bash
ipconfig getifaddr "$(scutil --nwi | scutil --nwi | awk '/IPv4/{getline;print $1;exit}')"
```
