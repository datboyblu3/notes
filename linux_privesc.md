### Run the following commands to enumerate a system

**Returns the hostname of the target machine**
```JavaScript
hostname
```
**Will print system information giving us additional detail about the kernel used by the system**
```JavaScript
uname -a
```

**The proc filesystem (procfs) provides information about the target system processes**
```JavaScript
/proc/version
```

**Usually contains some information about the operating system**
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

**List all commands your user can run using sudo**
```JavaScript
sudo -l
```
**General overview of the user’s privilege level and group memberships**
```JavaScript
id 
```

**Verify environment variables*
```JavaScript
env
```

**Potentially discover users on the system**
```JavaScript
/etc/passwd
```

**Cut away the fat from the command above**
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

**list TCP or UDP protocols **
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

**Folders and files that can be written to or executed from**
```JavaScript
find / -writable -type d 2>/dev/null
```
```JavaScript
find / -perm -222 -type d 2>/dev/null
```
```JavaScript
find / -perm -o w -type d 2>/dev/null
```

**Find world-executable folders**
```JavaScript
find / -perm -o x -type d 2>/dev/null
```

**Find development tools and supported languages**
```JavaScript
find / -name perl*
```
```JavaScript
find / -name python*
```
```JavaScript
find / -name gcc*
```

**Find files with the SUID bit**
```JavaScript
find / -perm -u=s -type f 2>/dev/null
```

```JavaScript
find / -type f -perm -04000 -ls 2>/dev/null
```

**Privilege Escalation with Sudo**

Run nano and press CTRL+R and CTRL+X. Then enter the following and press enter:
```JavaScript
reset; bash 1>&0 2>&0
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
