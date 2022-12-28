### Windows Users

**SYSTEM/LocalSystem**

An account used by the operating system to perform internal tasks. It has full access to all files and 

resources available on the host with even higher privileges than administrators.

**Local Service**

Default account used to run Windows services with "minimum" privileges. It will use anonymous connections over the network.

**Network Service**

Default account used to run Windows services with "minimum" privileges. It will use the computer credentials to authenticate through the network.

### Harvesting Passwords from Usual Spots

**Unattended Windows Installations**

When installing Windows on a large number of hosts, administrators may use Windows Deployment Services, which allows for a single operating system image to be deployed to several hosts through the network. These kinds of installations are referred to as unattended installations as they don't require user interaction. Such installations require the use of an administrator account to perform the initial setup, which might end up being stored in the machine in the following locations:

- C:\Unattend.xml
- C:\Windows\Panther\Unattend.xml
- C:\Windows\Panther\Unattend\Unattend.xml
- C:\Windows\system32\sysprep.inf
- C:\Windows\system32\sysprep\sysprep.xml
