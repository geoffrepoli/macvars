## Symantec Endpoint Protection

###### SEP VERSION
```
defaults read "/Applications/Symantec Solutions/Symantec Endpoint Protection.app/Contents/Info.plist" CFBundleShortVersionString
```

###### LAST AV SCAN
```bash
sqlite3 -line "/Library/Application Support/Symantec/SymUIAgent/Logs/SymAVLog" 'SELECT strftime("%Y-%m-%d %H:%M:%S",timeStamp,"unixepoch","localtime","+31 year") FROM LogEntry WHERE timeStamp = ( SELECT max(timeStamp) FROM LogEntry)' | awk -F'= ' '{print $NF}'
```
