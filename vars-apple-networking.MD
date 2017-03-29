###### ACTIVE NETWORK INTERFACE
```bash
scutil --nwi | grep -A1 "IPv4 network" | sed '1d' | awk '{print $1}'
```
###### ACTIVE NETWORK SERVICE
```bash
networksetup -listallhardwareports | grep "$(scutil --nwi | grep -A1 "IPv4 network" | sed '1d' | awk '{print $1}')" -B1 | awk -F': ' '/Hardware Port/{print $NF}'
```
###### ACTIVE MAC ADDRESS
```bash
networksetup -getmacaddress "$(scutil --nwi | grep -A1 "IPv4 network" | sed '1d' | awk '{print $1}')" | awk '{print $3}'
```
###### WI-FI INTERFACE
```bash
networksetup -listallhardwareports | grep -A1 Wi-Fi | awk '/Device/{print $NF}'
```
###### WI-FI POWER
```bash
networksetup -getairportpower "$(networksetup -listallhardwareports | grep -A1 Wi-Fi | awk '/Device/{print $NF}')" | awk '{print $NF}'
```
###### CURRENT SSID
```bash
networksetup -getairportnetwork "$(networksetup -listallhardwareports | grep -A1 Wi-Fi | awk '/Device/{print $2}')" 2> /dev/null | awk -F': ' '{print $NF}'
```
###### IP ADDRESS
```bash
ipconfig getifaddr "$(scutil --nwi | grep -A1 "IPv4 network" | sed '1d' | awk '{print $1}')"
```
