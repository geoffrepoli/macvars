## Jamf Info

###### COMPUTER NAME FROM JSS
```bash
/usr/local/bin/jamf getComputerName | awk -F'[<>]' '{print $3}'
```
