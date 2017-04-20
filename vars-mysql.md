###### MYSQL COMMUNITY VERSION
```bash
/usr/local/mysql/bin/mysql --version | awk '{print substr($5,1,length($5)-1)}'
```
