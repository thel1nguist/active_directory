# 01 - Installing the Domain Controller

1. Use `scconfig` to:
    - Change the hostname
    - Change the IP address to static
    - Change the DNS server to our own IP address

2. Install the Active Directory Windows Feature

```shell
Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
```

3. Configure AD and install Forest

```
import-Module ADDSDeployment

install ADDSForest

```

- Enter the Domain name (e.g. xyz.com), set the SafeModeAdministratorPassword (can be same as Domain Admin PW), confirm with 'Y'.


4. Configure the DC as DNS Server


- During installation, the DC sets the DNS to a loop address, and we have to change it back


```
Get-NetIPAddress -IPAddress [DC IP]

Get-DNSClientServerAddress

Set-DNSClientServerAddress -InterfaceIndex [if_index] -ServerAddresses [DC IP]

```

Double-check that the DNS IP changed: 

```
Get-DNSClientServerAddress
```

**XYZ Domain is now created and set up!**


# Joining the Workstation to the Domain


```
Add-Computer -DomainName xyz.com -Credential xyz\Administrator -Force -Restart
```