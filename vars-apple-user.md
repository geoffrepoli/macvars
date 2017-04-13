## User Info

###### LOGGED-IN USER NAME
```bash
/usr/bin/python -c 'from SystemConfiguration import SCDynamicStoreCopyConsoleUser; import sys; username = (SCDynamicStoreCopyConsoleUser(None, None, None) or [None])[0]; username = [username,""][username in [u"loginwindow", None, u""]]; sys.stdout.write(username + "\n");'
```

###### LOGGED-IN USER HOME
```bash
/usr/bin/dscl /Local/Default read /Users/<USER_SHORT_NAME> NFSHomeDirectory | awk -F': ' '{print $NF}'
# Note: the command above will not work if user is a network account
# The following workflow, while strange, will work on any user type:
loggedinuser=$(/usr/bin/python -c 'from SystemConfiguration import SCDynamicStoreCopyConsoleUser; import sys; username = (SCDynamicStoreCopyConsoleUser(None, None, None) or [None])[0]; username = [username,""][username in [u"loginwindow", None, u""]]; sys.stdout.write(username + "\n");'); loggerinuserhome=$(homedir=~"$loggedinuser"; eval homedir="$homedir"; echo "$homedir")
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
