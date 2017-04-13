## User Info

###### LOGGED-IN USER NAME
```bash
/usr/bin/python -c 'from SystemConfiguration import SCDynamicStoreCopyConsoleUser; import sys; username = (SCDynamicStoreCopyConsoleUser(None, None, None) or [None])[0]; username = [username,""][username in [u"loginwindow", None, u""]]; sys.stdout.write(username + "\n");'
# The remaining variables on this page are written with the assumptiont that you're assigning this command
# to a variable $loggedinuser. Ensure your workflow is configured appropriately
```

###### LOGGED-IN USER HOME
```bash
/usr/bin/dscl /Local/Default read /Users/<USER_SHORT_NAME> NFSHomeDirectory | awk -F': ' '{print $NF}'
# Note: the command above will not work if user is a network account
# The following workflow, while strange, will work on any user type.
# $userhome variable name is just a placeholder, feel free to change.
userhome=$(h=~"$loggedinuser" ; eval h="$h" ; echo "$h")
```

###### LOGGED-IN TIME *(reported in decimal hours)*
```bash
/usr/sbin/ac -p | grep -w "$loggedinuser" | awk '{print $NF}'
```

###### TOUCH ID STATUS
```bash
/usr/bin/bioutil -c -s | grep -wE "${loggedinuser}|$(id -u "$loggedinuser")"
# only available on Macs with Touch Bar
```
