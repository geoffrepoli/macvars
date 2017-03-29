###### ACTIVE DIRECTORY DOMAIN
```bash
dsconfigad -show | awk -F'= ' '/Active Directory Domain/{print $NF}'
```

###### ACTIVE DIRECTORY FOREST
```bash
dsconfigad -show | awk -F'= ' '/Active Directory Forest/{print $NF}'
```

###### COMPUTER ACCOUNT
```bash
dsconfigad -show | awk -F'= ' '/Computer Account/{print $NF}'
```

###### ALLOWED ADMIN GROUPS
```bash
dsconfigad -show | awk -F'= ' '/admin groups/{print $NF}'
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
dsconfigad -show | awk -F'= ' '/Packet signing/{print $NF}'
```

###### PACKET ENCRYPTION
```bash
dsconfigad -show | awk -F'= ' '/Packet encryption/{print $NF}'
```
