## User Info

###### LOGGED-IN USER NAME
```bash
/usr/bin/python -c 'from SystemConfiguration import SCDynamicStoreCopyConsoleUser; import sys; username = (SCDynamicStoreCopyConsoleUser(None, None, None) or [None])[0]; username = [username,""][username in [u"loginwindow", None, u""]]; sys.stdout.write(username + "\n");'
```

###### LOGGED-IN USER HOME
```bash
dscl . read /Users/<USER_SHORT_NAME> NFSHomeDirectory
```
###### *note: the following trick can be used for network users as well, since `~` + `username` expands to `username`'s home directory. Set variable = to:*
```bash
$(homedir=~<USER_SHORT_NAME>; eval homedir="$homedir"; echo "$homedir")
```

###### LOGGED-IN TIME *(reported in decimal hours)*
```bash
ac -p | grep -w <USER_SHORT_NAME> | awk '{print $NF}'
```

###### TOUCH ID STATUS *(if true, then... e.g.,: `[ $VAR ] && echo Enabled`)*
```bash
bioutil -c -s | grep -wE "<USER_SHORT_NAME>|$(id -u <USER_SHORT_NAME>)"
```
