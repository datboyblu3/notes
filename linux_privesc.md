### Run the following commands to enumerate a system

```JavaScript
hostname
```

```JavaScript
uname -a
```

```JavaScript
/proc/version
```

```JavaScript
/etc/issue
```

**View all running processes**
```JavaScript
ps -A
```
**View process tree**
```JavaScript
ps axjf
```

**View processes for all users**
```JavaScript
ps aux
```

```JavaScript
sudo -l
```

```JavaScript
id 
```

```JavaScript
/etc/passwd
```

```JavaScript
cat /etc/passwd | grep home
```

**View network routes**
```JavaScript
ip route
```

**Show all listening ports and established connections**
```JavaScript
netstat -a
```

**Show all listening TCP and UDP ports and established connections**
```JavaScript
netstat -at 
```

```JavaScript
netstat -au
```

**List ports in listening mode**
```JavaScript
netstat -l
```
**List network usage statistics by protocol **
```JavaScript
netstat -s
```

**List connections with the service name and PID information**
```JavaScript
netstat -tp
```
**Show interface statistics**
```JavaScript
netstat -i
```

**Netstat. Display all sockets, Do no resolve names, Display timers**
```JavaScript
netstat -ano
```

**find the file named “flag1.txt” in the current directory**
```JavaScript
find . -name flag1.txt
```

**find the file names “flag1.txt” in the /home directory**
```JavaScript
find /home -name flag1.txt
```

**find the directory named config under “/”**
```JavaScript
find / -type d -name config
```

**find files with the 777 permissions (files readable, writable, and executable by all users)**
```JavaScript
find / -type f -perm 0777
```

**find executable files**
```JavaScript
find / -perm a=x
```

**find all files for user “frank” under “/home”**
```JavaScript
find /home -user frank
```

**find files that were modified in the last 10 days**
```JavaScript
find / -mtime 10
```

**find files that were accessed in the last 10 day**
```JavaScript
find / -atime 10
```

**find files changed within the last hour (60 minutes)**
```JavaScript
find / -cmin -60
```

**find files accesses within the last hour (60 minutes)**
```JavaScript
find / -amin -60
```

**find files with a 50 MB size**
```JavaScript
find / -size 50M
```

****
```JavaScript

```

****
```JavaScript

```

****
```JavaScript

```

****
```JavaScript

```

****
```JavaScript

```

****
```JavaScript

```

****
```JavaScript

```

****
```JavaScript

```

****
```JavaScript

```

