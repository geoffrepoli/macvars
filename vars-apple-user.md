## User Info

###### LOGGED-IN USER NAME
```bash
/usr/bin/python -c 'from SystemConfiguration import SCDynamicStoreCopyConsoleUser; import sys; username = (SCDynamicStoreCopyConsoleUser(None, None, None) or [None])[0]; username = [username,""][username in [u"loginwindow", None, u""]]; sys.stdout.write(username + "\n");'
```

###### LOGGED-IN USER HOME
```bash
/usr/bin/dscl /Local/Default read /Users/<USER_SHORT_NAME> NFSHomeDirectory | awk -F': ' '{print $NF}'
# Note: the command above will not work if user is a network account
# The following workflow, while strange, will work on any user type. Ensure you assign a
# value to the $loggedinuser variable (e.g., use the LOGGED-IN USER NAME command above).
# "userhome" variable name is just a placeholder, feel free to replace it.
userhome=$(h=~"$loggedinuser" ; eval h="$h" ; echo "$h")
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
