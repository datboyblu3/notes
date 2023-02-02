## Active Directory

Active Directory is a Windows-based directory service that stores and provides data objects to the internal network environment. 
It allows for centralized management of authentication and authorization. The AD contains essential information about the network 
and the environment, including users, computers, printers, etc. For example, AD might have users' details such as job title, phone number, 
address, passwords, groups, permission, etc

![59664b98a3a0b01cf6b7e83e039ddb84](https://user-images.githubusercontent.com/95729902/216198985-e5d0fe61-5cac-47af-9c84-ab3e24509b74.png)

The diagram is one possible example of how Active Directory can be designed. The AD controller is placed in a subnet for servers 
(shown above as server network), and then the AD clients are on a separate network where they can join the domain and use the AD services via the firewall.

**Domain Controller**
- a Windows server that provides Active Directory services and controls the entire domain
- is a form of centralized user management that provides encryption of user data as well as controlling access to a network, including users, groups, policies, and computers
- enables resource access and sharing

![c982e300552d540f0fc456cc05be21cd](https://user-images.githubusercontent.com/95729902/216199548-28cd7464-551a-446b-8e11-342819743043.png)


**Organizational Units**

Are contrainers within the AD domain with a hierchical structure

**Active Directory Objects**

- can be a single user or a group, or a hardware component, such as a computer or printer. Each domain holds a database that contains object identity information that creates an AD environment, including:
  - users: A security principal that is allowed to authenticate to machines in the domain
  - Computers - a special type of user accounts
  - GPOs - Collections of policies that are applied to other AD objects

**AD domains**: are a collection of Microsoft components within an AD network

**AD Forest*: a collection of domains that trust each other

![bb4bec81a78f745e8cbc38f7879002dd](https://user-images.githubusercontent.com/95729902/216200280-fa570bc0-abc4-4635-b13b-dff2a0c56f56.png)

## Users and Groups Management

- The built-in local users' accounts are used to manage the system locally, which is not part of the AD environment.
- Domain user accounts with access to an active directory environment can use the AD services (managed by AD).
- AD managed service accounts are limited domain user account with higher privileges to manage AD services.
- Domain Administrators are user accounts that can manage information in an Active Directory environment, including AD configurations, users, groups, permissions, roles, services, etc. One of the red team goals 
in engagement is to hunt for information that leads to a domain administrator having complete control over the AD environment.



| Account | Description |
| ----------- | ----------- |
| BUILTIN\Administrator | Local admin access on a domain controller |
| Domain Admins | Administrative access to all resources in the domain |
| Enterprise Admins | Enterprise Admins |
| Schema Admins | Capable of modifying domain/forest; useful for red team |
| Server Operators | Can manage domain servers |
| Account Operators | Can manage users that are not in privileged groups |

## Active Directory Enumeration

**Get All AD User Accounts**
```PowerShell
Get-ADUser -Filter *
```

The Distinguished Name (DN) is a collection of comma-separated key and value pairs used to identify unique records within the directory. The DN consists of Domain Component (DC), OrganizationalUnitName (OU), Common Name (CN), and others. The following "CN=User1,CN=Users,DC=thmredteam,DC=com" is an example of DN, which can be visualized as follow:

![764c72d40ec3d823b05d6473702e00f5](https://user-images.githubusercontent.com/95729902/216207218-74d45940-a495-41f9-9f8a-5aa48ca9caf8.png)


Using the SearchBase option, we specify a specific Common-Name CN in the active directory. For example, we can specify to list any user(s) that part of Users:

```PowerShell
Get-ADUser -Filter * -SearchBase "CN=Users,DC=THMREDTEAM,DC=COM"
```

