## Jamf Info

###### COMPUTER NAME FROM JSS
```bash
/usr/local/jamf/bin/jamf getComputerName | awk -F'[<>]' '{print $3}'
```
