## Mac User Information

##### LOGGED-IN USER NAME
```bash
/usr/bin/python -c 'from SystemConfiguration import SCDynamicStoreCopyConsoleUser; import sys; username = (SCDynamicStoreCopyConsoleUser(None, None, None) or [None])[0]; username = [username,""][username in [u"loginwindow", None, u""]]; sys.stdout.write(username + "\n");'
# The remaining variables on this page are written with the assumptiont that you're assigning this command
# to a variable $loggedinuser. Ensure your workflow is configured appropriately
```

##### LOGGED-IN USER HOME
```bash
dscl . read /users/$loggedInUser NFSHomeDirectory | cut -d' ' -f2
# Note: the command above will not work if user is a network account
# The following workflow, while strange, will work on any user type.
# $userhome variable name is just a placeholder, feel free to change.
userhome=$(h=~"$loggedinuser" ; eval h="$h" ; echo "$h")
```

##### LOGGED-IN TIME
```bash
ac -p | awk -v u=$loggedInUser '$0~u{print $2}'
# NOTE: As of 10.12.4 this command no longer accurately reports logged-in time. Appears it uses
# utmp/wtmp, which were deprecated in 10.12 and appear to be no longer used in 10.12.4
```

##### LAST AD PASSWORD CHANGE DATE
```bash
dscl localhost read /Search/Users/$loggedInUser SMBPasswordLastSet | awk 'END{printf "%.0f",($NF/10000000)-11644473600}' | xargs -I{} date -r {} "+%F %T %Z"
```

##### TOUCH ID STATUS
```bash
bioutil -c -s | grep -wE "$loggedInUser|$(id -u $loggedInUser)" | cut -f2
# only available on Macs with Touch Bar, must run as root
```

##### GET ALL LOCAL/MOBILE USERS
```bash
dscl . list /users uid | awk '$2>=499{print $1}'
# add to an array with users+=( $(dscl . list /users uid | awk '$2>=499{print $1}') )
```
