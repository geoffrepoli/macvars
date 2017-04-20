## macOS Software

###### OS VERSION
```bash
/usr/bin/sw_vers -productVersion
```

###### OS VERSION - MAJOR
```bash
/usr/bin/sw_vers -productVersion | awk -F. '{print $2}'
```

###### OS VERSION - MINOR
```bash
/usr/bin/sw_vers -productVersion | awk -F. '{print $3}'
```

###### BUILD NUMBER
```bash
/usr/bin/sw_vers -buildVersion
```

###### SOFTWARE UPDATE SERVER
```bash
/usr/bin/defaults read /Library/Preferences/com.apple.SoftwareUpdate.plist CatalogURL 2> /dev/null

# note: key does not exist if set to default, thus 2> /dev/null will prevent using stderr
```

###### AUTOMATIC UPDATES ENABLED
```bash
/usr/bin/defaults read /Library/Preferences/com.apple.SoftwareUpdate.plist AutomaticCheckEnabled
```
