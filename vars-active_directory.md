## Active Directory

###### ACTIVE DIRECTORY DOMAIN
```bash
/usr/sbin/dsconfigad -show | awk -F'= ' '/Active Directory Domain/{print $NF}'
```

###### ACTIVE DIRECTORY FOREST
```bash
/usr/sbin/dsconfigad -show | awk -F'= ' '/Active Directory Forest/{print $NF}'
```

###### COMPUTER ACCOUNT
```bash
/usr/sbin/dsconfigad -show | awk -F'= ' '/Computer Account/{print $NF}'
```

###### ALLOWED ADMIN GROUPS
```bash
/usr/sbin/dsconfigad -show | awk -F'= ' '/admin groups/{print $NF}'
```

###### NETWORK PROTOCOL
```bash
/usr/sbin/dsconfigad -show | awk -F'= ' '/protocol/{print $NF}'
```

###### USING MOBILE ACCOUNTS
```bash
/usr/sbin/dsconfigad -show | awk -F'= ' '/mobile/{print $NF}'
```

###### USING LOCAL HOMES
```bash
/usr/sbin/dsconfigad -show | awk -F'= ' '/startup/{print $NF}'
```

###### PACKET SIGNING
```bash
/usr/sbin/dsconfigad -show | awk -F'= ' '/Packet signing/{print $NF}'
```

###### PACKET ENCRYPTION
```bash
/usr/sbin/dsconfigad -show | awk -F'= ' '/Packet encryption/{print $NF}'
```
