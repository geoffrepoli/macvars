## Active Directory

###### ACTIVE DIRECTORY DOMAIN
```bash
dsconfigad -show | awk -F'= ' '/A.*D.*Do/{print $NF}'
```

###### ACTIVE DIRECTORY FOREST
```bash
dsconfigad -show | awk -F'= ' '/A.*D.*Fo/{print $NF}'
```

###### COMPUTER ACCOUNT
```bash
dsconfigad -show | awk -F'= ' '/Co.*Ac/{print substr($NF,1,length($NF)-1)}'
```

###### ALLOWED ADMIN GROUPS
```bash
dsconfigad -show | awk -F'= ' '/ad.*gr/{print $NF}'
```

###### NETWORK PROTOCOL
```bash
dsconfigad -show | awk -F'= ' '/protocol/{print $NF}'
```

###### USING MOBILE ACCOUNTS
```bash
dsconfigad -show | awk -F'= ' '/mobile/{print $NF}'
```

###### USING LOCAL HOMES
```bash
dsconfigad -show | awk -F'= ' '/startup/{print $NF}'
```

###### PACKET SIGNING
```bash
dsconfigad -show | awk -F'= ' '/Pa.*si/{print $NF}'
```

###### PACKET ENCRYPTION
```bash
dsconfigad -show | awk -F'= ' '/P.*en/{print $NF}'
```
