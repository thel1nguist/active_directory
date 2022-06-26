# 00 - Install VMs

1. Installed Windows Server 2019 as a Virtual machine in ORACLE VirtualBox.
2. Installed Windows 11 Workstation as a Virtual machine in ORACLE VirtualBox.

# Setup Remote Powershell Session from Management Client to DC

 ```shell
 Enable-PSRemoting
 
 Start-Service WinRM
 
 set-item wsman:\localhost\Client\TrustedHosts -value [Domain Contr. IP]
 
 New-PSSession -ComputerName [DC IP] -Credential (Get-Credential)
 
 ```

 - Enter DC Password  
   
    
```
Enter-PSSession 1
```