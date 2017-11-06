## Jamf Info

###### COMPUTER NAME FROM JSS
```bash
/usr/local/bin/jamf getComputerName | awk -F'[<>]' '{print $3}'
```

###### JSS COMPUTER ID
```bash
uuid=$(ioreg -rd1 -c IOPlatformExpertDevice | awk -F\" '/UUID/{print $(NF-1)}')
curl -skX GET -u $jssuser:$jsspass $jssurl/JSSResource/computers/udid/$uuid | xmllint --xpath "string(/computer/general/id)" -
```
