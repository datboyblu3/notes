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

**Powershell History**

Whenever a user runs a command using Powershell, it gets stored into a file that keeps a memory of past commands. This is useful for repeating commands you have used before quickly. If a user runs a command that includes a password directly as part of the Powershell command line, it can later be retrieved by using the following command from a cmd.exe prompt:

*To read the file from Powershell, you'd have to replace %userprofile% with $Env:userprofile*
```JavaScript
%userprofile%\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt
```

**Saved Windows Credentials**

The command below will list saved credentials. 

```JavaScript
cmdkey /list
```

Although you wont be able to see the credentials, use the *runas* command and the */savecred* option/
```JavaScript
runas /savecred /usr:admin cmd.exe
```

**IIS Configuration**

Internet Information Services (IIS) is the default web server on Windows installations. The configuration of websites on IIS is stored in a file called web.config and can store passwords for databases or configured authentication mechanisms. Depending on the installed version of IIS, we can find web.config in one of the following locations:

- C:\inetpub\wwwroot\web.config
- C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\web.config

```JavaScript
type C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\web.config | findstr connectionString
```

**Retrieve Credentials from Software: PuTTY**

PuTTY is an SSH client commonly found on Windows systems. Instead of having to specify a connection's parameters every single time, users can store sessions where the IP, user and other configurations can be stored for later use. While PuTTY won't allow users to store their SSH password, it will store proxy configurations that include cleartext authentication credentials.

To retrieve the stored proxy credentials, you can search under the following registry key for ProxyPassword with the following command:

```JavaScript
reg query HKEY_CURRENT_USER\Software\SimonTatham\PuTTY\Sessions\ /f "Proxy" /s
```

### Scheduled Tasks

Scheduled tasks can be listed from the command line using the schtasks command without any options. To retrieve detailed information about any of the services, you can use a command like the following one:

```JavaScript
schtasks /query /tn vulntask /fo list /v
```



```JavaScript

```

## Abusing Service Misconfigurations

Windows services are managed by the Service Control Manager (SCM). The SCM is a process in charge of managing the state of services as needed, checking the current status of any given service and generally providing a way to configure services.

Each service on a Windows machine will have an associated executable which will be run by the SCM whenever a service is started. It is important to note that service executables implement special functions to be able to communicate with the SCM, and therefore not any executable can be started as a service successfully. Each service also specifies the user account under which the service will run.

Services have a Discretionary Access Control List (DACL), which indicates who has permission to start, stop, pause, query status, query configuration, or reconfigure the service, amongst other privileges.

All of the services configurations are stored on the registry under HKLM\SYSTEM\CurrentControlSet\Services\ .


## SeBackup / SeRestore

The SeBackup and SeRestore privileges allow users to read and write to any file in the system, ignoring any DACL in place. The idea behind this privilege is to allow certain users to perform backups from a system without requiring full administrative privileges.

**Verfiy your privileges**

```JavaScript
whoami /priv
```

**To backup the SAM and SYSTEM hashes, we can use the following commands**

```JavaScript
reg save hklm\system C:\Users\THMBackup\system.hive

reg save hklm\sam C:\Users\THMBackup\sam.hive
```

This will create a couple of files with the registry hives content. We can now copy these files to our attacker machine using SMB or any other available method. For SMB, we can use impacket's smbserver.py to start a simple SMB server with a network share in the current directory of our AttackBox:

```JavaScript
mkdir share

python3.9 /opt/impacket/examples/smbserver.py -smb2support -username THMBackup -password CopyMaster555 public share
```

