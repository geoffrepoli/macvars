## Mac Network Information

###### ACTIVE NETWORK DEVICE (e.g., en0)
```bash
scutil --nwi | awk '/IPv4/{getline;print $1;exit}'
```

###### ACTIVE NETWORK SERVICE (e.g., Wi-Fi)
```bash
networksetup -listallhardwareports | awk -F': ' -v d=$(scutil --nwi | awk '/IPv4/{getline;print $1;exit}') '$0~d{print a}{a=$NF}'
```

###### ACTIVE MAC ADDRESS
```bash
networksetup -getmacaddress $(scutil --nwi | awk '/IPv4/{getline;print $1;exit}') | awk '{print $3}'
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
ipconfig getifaddr "$(scutil --nwi | awk '/IPv4/{getline;print $1;exit}')"
```
