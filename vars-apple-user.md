## User Info

###### LOGGED-IN USER NAME
```bash
/usr/bin/python -c 'from SystemConfiguration import SCDynamicStoreCopyConsoleUser; import sys; username = (SCDynamicStoreCopyConsoleUser(None, None, None) or [None])[0]; username = [username,""][username in [u"loginwindow", None, u""]]; sys.stdout.write(username + "\n");'
# The remaining variables on this page are written with the assumptiont that you're assigning this command
# to a variable $loggedinuser. Ensure your workflow is configured appropriately
```

###### LOGGED-IN USER HOME
```bash
/usr/bin/dscl /Local/Default read /Users/"$loggedinuser" NFSHomeDirectory | awk -F': ' '{print $NF}'
# Note: the command above will not work if user is a network account
# The following workflow, while strange, will work on any user type.
# $userhome variable name is just a placeholder, feel free to change.
userhome=$(h=~"$loggedinuser" ; eval h="$h" ; echo "$h")
```

###### LOGGED-IN TIME
```bash
/usr/sbin/ac -p | grep -w "$loggedinuser" | awk '{print $NF}'
# NOTE: As of 10.12.4 this command no longer accurately reports logged-in time. Appears it uses
# utmp/wtmp, which were deprecated in 10.12 and appear to be no longer used in 10.12.4
```

###### TOUCH ID STATUS
```bash
/usr/bin/bioutil -c -s | grep -wE "${loggedinuser}|$(id -u "$loggedinuser")"
# only available on Macs with Touch Bar
```

###### LOCAL ADMINS
```bash
for USERNAME in $(dscl . read /groups/admin GroupMembership | sed 's/GroupMembership: //')
do [ "$USERNAME" != root ] && ADMIN+=( "$USERNAME" )
done
# this creates an array of all local admins (excluding root), which can be called 
# with variable ${ADMIN[@]}
```
