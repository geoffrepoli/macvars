## Active Directory

###### ACTIVE DIRECTORY DOMAIN
```bash
dsconfigad -show | awk '/A*Dir.*D/{print $NF}'
```

###### ACTIVE DIRECTORY FOREST
```bash
dsconfigad -show | awk '/A*Dir.*F/{print $NF}'
```

###### COMPUTER ACCOUNT
```bash
dsconfigad -show | awk '/Com.*Acc/{print substr($NF,1,length($NF)-1)}'
```

###### ALLOWED ADMIN GROUPS
```bash
dsconfigad -show | awk -F'= ' '/ad.*groups/{print $NF}'
```

###### NETWORK PROTOCOL
```bash
dsconfigad -show | awk '/protocol/{print $NF}'
```

###### USING MOBILE ACCOUNTS
```bash
dsconfigad -show | awk '/mobile/{print $NF}'
```

###### USING LOCAL HOMES
```bash
dsconfigad -show | awk '/startup/{print $NF}'
```

###### PACKET SIGNING
```bash
dsconfigad -show | awk -F'= ' '/Pa.*sig/{print $NF}'
```

###### PACKET ENCRYPTION
```bash
dsconfigad -show | awk -F'= ' '/Pa.*enc/{print $NF}'
```
