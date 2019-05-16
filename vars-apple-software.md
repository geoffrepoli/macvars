## macOS & Mac Software Update Information

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

###### FRONTMOST APP
```bash
osascript -e 'tell app "System Events" to return name of first application process whose frontmost is true'
```

###### LIST ALL 32-BIT APPLICATIONS
```bash
while IFS= read -r app; do file "$app"/Contents/MacOS/* | awk -F: '!/for/&&/i386/&&!/x86_64/{gsub(/\ /,"\\ ");print $1}'; done < <(find -x / -path /System -prune -o -name "*.app" 2> /dev/null)
```

###### SOFTWARE UPDATE SERVER
```bash
defaults read /Library/Preferences/com.apple.SoftwareUpdate.plist CatalogURL 2> /dev/null

# note: key does not exist if set to default, thus 2> /dev/null will prevent using stderr
```

###### AUTOMATIC UPDATES ENABLED
```bash
defaults read /Library/Preferences/com.apple.SoftwareUpdate.plist AutomaticCheckEnabled
```
