## User Info

###### LOGGED-IN USER NAME
```bash
/usr/bin/python -c 'from SystemConfiguration import SCDynamicStoreCopyConsoleUser; import sys; username = (SCDynamicStoreCopyConsoleUser(None, None, None) or [None])[0]; username = [username,""][username in [u"loginwindow", None, u""]]; sys.stdout.write(username + "\n");'
```

###### LOGGED-IN USER HOME
```bash
/usr/bin/dscl /Local/Default read /Users/<USER_SHORT_NAME> NFSHomeDirectory | awk -F': ' '{print $NF}'
# will not work for network users. the following will get the home directory of any user, including network:
`homedir=~<USER_SHORT_NAME>; eval homedir="$homedir"; echo "$homedir"`
```

###### LOGGED-IN TIME *(reported in decimal hours)*
```bash
/usr/sbin/ac -p | grep -w <USER_SHORT_NAME> | awk '{print $NF}'
```

###### TOUCH ID STATUS
```bash
/usr/bin/bioutil -c -s | grep -wE "<USER_SHORT_NAME>|$(id -u <USER_SHORT_NAME>)"
# only available on Macs with Touch Bar
```
