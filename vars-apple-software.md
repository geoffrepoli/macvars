## macOS Software

###### OS VERSION
```bash
sw_vers -productVersion
```

###### OS VERSION - MAJOR
```bash
sw_vers -productVersion | awk -F. '{print $2}'
```

###### OS VERSION - MINOR
```bash
sw_vers -productVersion | awk -F. '{print $3}'
```

###### BUILD NUMBER
```bash
sw_vers -buildVersion
```

###### SOFTWARE UPDATE SERVER *(key does not exist if set to default)*
```bash
defaults read /Library/Preferences/com.apple.SoftwareUpdate.plist CatalogURL
```

###### AUTOMATIC UPDATES ENABLED
```bash
defaults read /Library/Preferences/com.apple.SoftwareUpdate.plist AutomaticCheckEnabled
```
