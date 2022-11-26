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

