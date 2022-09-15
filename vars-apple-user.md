## Mac User Information

##### LOGGED-IN USER NAME
```bash
stat -f%Su /dev/console
# The remaining variables on this page are written with the assumptiont that you're assigning this command
# to a variable $loggedinuser. Ensure your workflow is configured appropriately
```

##### LOGGED-IN USER UID
```bash
stat -f%u /dev/console
```

##### LOGGED-IN USER HOME
```bash
dscl . read /users/$(stat -f%Su /dev/console) NFSHomeDirectory | cut -d' ' -f2-
```

##### TOUCH ID ENABLED
```bash
bioutil -c -s | grep -wE "$(stat -f%Su /dev/console)|$(stat -f%u /dev/console)" | cut -f2
```

##### TOUCH ID TIMEOUT IN SECONDS
```bash
bioutil -r -s | awk -F': ' '/timeout/{print $NF}'
```

##### LAST AD PASSWORD CHANGE DATE FOR MOBILE ACCOUNT
```bash
dscl localhost read /Search/Users/$(stat -f%Su /dev/console) SMBPasswordLastSet | awk 'END{printf "%.0f",($NF/10000000)-11644473600}' | xargs -I{} date -r {} "+%F %T %Z"
```

##### GET ALL LOCAL/MOBILE USERS
```bash
dscl . list /users uid | awk '$2>=499{print $1}'
# add to an array with users+=( $(dscl . list /users uid | awk '$2>=499{print $1}') )
```

##### USER IDLE TIME
```bash
ioreg -rd1 -c IOHIDSystem | awk '/HIDIdleTime/{printf "%1.0f\n",$NF/1000000000}'
# use in a while loop: `while (( $(ioreg -rd1 -c IOHIDSystem | awk '/HIDIdleTime/{printf "%1.0f\n",$NF/1000000000}') < [time in seconds] )); do sleep 0.1; done`
```
