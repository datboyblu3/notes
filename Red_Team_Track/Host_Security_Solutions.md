Before performing further actions, we need to obtain general knowledge about the security solutions in place. Remember, 
it is important to enumerate antivirus and security detection methods on an endpoint in order to stay as undetected as possible 
and reduce the chance of getting caught.

Enumerate antivirus like so:

```PowerShell
 wmic /namespace:\\root\securitycenter2 path antivirusproduct
```

```PowerShell
Get-CimInstance -Namespace root/SecurityCenter2 -ClassName AntivirusProduct
```



## Microsoft Windows Defender

Microsoft Windows Defender is a pre-installed antivirus security tool that runs on endpoints. It uses various algorithms in the detection, 
including machine learning, big-data analysis, in-depth threat resistance research, and Microsoft cloud infrastructure in protection against 
malware and viruses. MS Defender works in three protection modes: Active, Passive, Disable modes. 

Active mode is used where the MS Defender runs as the primary antivirus software on the machine where provides protection and remediation. 
Passive mode is run when a 3rd party antivirus software is installed. Therefore, it works as secondary antivirus software where it scans 
files and detects threats but does not provide remediation. Finally, Disable mode is when the MS Defender is disabled or uninstalled from the system.

 Use the following PowerShell command to check the service state of Windows Defender:
 
 ```PowerShell
 Get-Service WinDefend
 ```
 
 Next, we can start using the Get-MpComputerStatus cmdlet to get the current Windows Defender status. However, it provides the current status of security 
 solution elements, including Anti-Spyware, Antivirus, LoavProtection, Real-time protection, etc. We can use select to specify what we need for as follows:
 
 ```PowerShell
 Get-MpComputerStatus | select RealTimeProtectionEnabled
 ```
 
 Enumerate Firewall Profiles
 
 ```PowerShell
 Get-NetFirewallProfile | Format-Table Name, Enabled
 ```
 
 If we have admin privileges on the current user we logged in with, then we try to disable one or more than one firewall profile using the Set-NetFirewallProfile cmdlet:
 
 ```PowerShell
 Set-NetFirewallProfile -Profile Domain, Public, Private -Enabled False
 Get-NetFirewallProfile | Format-Table Name, Enabled
 ```
 
 Get-NetFirewallRule | select DisplayName, Enabled, Description
 
 ```PowerShell
 Get-NetFirewallRule | select DisplayName, Enabled, Description
 ```
 
 During the red team engagement, we have no clue what the firewall blocks. However, we can take advantage of some PowerShell cmdlets such as Test-NetConnection and TcpClient. 
 Assume we know that a firewall is in place, and we need to test inbound connection without extra tools, then we can do the following: 
 
 ```PowerShell
 Test-NetConnection -ComputerName 127.0.0.1 -Port 80
 ```
