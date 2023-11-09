---
layout: post
title: "Building a Secure Active Directory with PowerShell"
date: 2023-11-09
categories: [Active Directory, PowerShell]
tags: [Active Directory, PowerShell, Security]
excerpt: This in-depth guide explores how to set up a secure Active Directory environment using PowerShell, with a focus on security best practices.
---

## Introduction

Welcome to this guide on establishing a secure Active Directory (AD) domain using PowerShell. As we navigate through the setup, we'll incorporate security best practices to fortify our domain against cyber threats. Ensuring a secure configuration from the outset is critical for a resilient network infrastructure.

## Prerequisites

Before we begin, make sure you have:

- A Windows Server 2012 R2 or later
- Administrative access to the server
- PowerShell with the AD module available

## Step 1: Installing Active Directory Domain Services Role

Our first move towards a robust AD environment is to install the Active Directory Domain Services role. This is the cornerstone that brings all the essential features we need to construct our domain.

```powershell
Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
```

## Step 2: Promoting the Server to a Domain Controller

With the AD Domain Services role in place, our next step is to elevate our server's status to that of a domain controller. This promotion is essential—it gives us the control center for managing our domain and enforcing centralized security policies.

```powershell
Import-Module ADDSDeployment
Install-ADDSForest `
-CreateDnsDelegation:$false `
-DatabasePath "C:\\Windows\\NTDS" `
-DomainMode "WinThreshold" `
-DomainName "example.com" `
-DomainNetbiosName "EXAMPLE" `
-ForestMode "WinThreshold" `
-InstallDns:$true `
-LogPath "C:\\Windows\\NTDS" `
-SysvolPath "C:\\Windows\\SYSVOL" `
-Force:$true
```

**Why This Matters**: When we promote our server to a domain controller, we're setting up the core components like the AD database and SYSVOL. It also marks our server as the go-to source for domain information. Including the DNS role is just as vital since AD depends on DNS for locating services and supporting domain operations efficiently.

## Step 3: Securing Time Synchronization with NTP

Precise timekeeping isn't just a convenience—it's a cornerstone of Active Directory security, especially for protocols like Kerberos authentication. It's crucial for our domain controller to maintain synchronization with a dependable external NTP source to ensure the integrity and security of authentication processes.

```powershell
w32tm /config /manualpeerlist:"time.nist.gov" /syncfromflags:manual /reliable:YES /update
Restart-Service w32time
```

**Why This Matters**: Kerberos, the authentication protocol at the heart of AD, is highly sensitive to time discrepancies. A difference exceeding five minutes can lead to authentication failures, or even expose our network to replay attacks. Configuring a reliable external NTP source is our safeguard, aligning our domain's timekeeping with a secure standard.

## Step 4: Establishing Robust AD Security Policies

Effective security policies act as a shield against unauthorized access, so it's imperative that we implement stringent password and account lockout policies. These measures are critical for fortifying user accounts within our domain against intrusion attempts.

```powershell
# Define a strong password policy
$PasswordPolicy = @{
    Name = "StrongPasswordPolicy"
    Description = "Enforces password complexity and history."
}
$PasswordPolicyGPO = New-GPO @PasswordPolicy
Set-GPPermission -Name $PasswordPolicyGPO.Name -PermissionLevel GpoEdit -TargetName "Domain Admins"
New-GPLink -Name $PasswordPolicyGPO.Name -Target "DC=example,DC=com"
# Apply the password policy
Set-ADDefaultDomainPasswordPolicy -ComplexityEnabled $true -LockoutDuration "00:30:00" -LockoutObservationWindow "00:30:00" -LockoutThreshold 5 -MaxPasswordAge "42.00:00:00" -MinPasswordAge "1.00:00:00" -MinPasswordLength 12 -PasswordHistoryCount 24 -ReversibleEncryptionEnabled $false
```

**Why This Matters**: Strong password and account lockout policies are our bulwark against brute-force attacks. Mandating complex passwords and defining lockout thresholds helps us to mitigate the risk of credential compromise, making it much harder for unauthorized entities to gain access to our domain.

## Step 5: Installing a Certificate for LDAP Server Authentication

Before we can enable LDAPS (LDAP over SSL), we must install a certificate that is valid for LDAP server authentication on our server. This certificate ensures that the communication over LDAP is encrypted and secure. 

**Note**: You can obtain a certificate from a public Certificate Authority (CA) or your internal CA if you have one.

```powershell
# Step 1: Obtain a certificate from a CA. This step varies depending on your CA.
# Make sure the certificate includes the server's fully qualified domain name (FQDN) in the Subject or Subject Alternative Name field.

# Step 2: Import the certificate into the local computer's Personal store.
Import-Certificate -FilePath "path\to\your\certificate.cer" -CertStoreLocation Cert:\LocalMachine\My
```

**Why This Matters**: LDAPS requires a certificate to create a secure channel over which to transmit data. Without this certificate, the data would be sent in plain text, which could expose sensitive information to anyone who is listening on the network.

## Step 6: Enabling Secure LDAP (LDAPS)

Now that we have installed the necessary certificate, we can proceed to enable LDAPS to secure our LDAP traffic.

```powershell
# Restart the Active Directory Domain Services to recognize the new certificate for LDAPS
Restart-Service NTDS -Force

# Confirm that LDAPS is working
Test-NetConnection -Port 636 -ComputerName <YourDomainController>
```

**Why This Matters**: By enabling LDAPS, you are ensuring that all communication between LDAP clients and your server is encrypted, preventing potential eavesdropping or man-in-the-middle attacks. It's a critical security measure for protecting authentication and directory queries.


## Step 7: Automating AD Deployment and Configuration

With the foundational elements of our Active Directory domain in place, it is time to introduce efficiency and consistency into our deployment process. Automation is key in any modern IT environment, and PowerShell offers us the tools necessary to achieve this. In this step, we will consolidate our previous manual tasks into a single, executable PowerShell script. This script will ensure that our secure AD setup can be replicated accurately and swiftly, reducing the potential for human error and streamlining the setup process.

This script includes everything from installing necessary roles, promoting our server to a domain controller, configuring time synchronization, establishing security policies, to enabling LDAP over SSL. By the end of this automated process, you will have a domain controller configured with security best practices in mind, ready to serve as the cornerstone of your secure network infrastructure.

Please review the script carefully, ensuring that all parameters are appropriately set for your specific environment before execution. The automation script is designed to run with administrative privileges and requires a preliminary setup of the correct execution policy.

`AD_Deployment_Script.ps1`

```powershell
# Step 1: Install AD Domain Services
Install-WindowsFeature AD-Domain-Services -IncludeManagementTools

# Step 2: Promote Server to Domain Controller
# Make sure to customize the domain name and safe mode administrator password
$domainName = "example.com"
$safeModeAdministratorPassword = ConvertTo-SecureString "YourPassword" -AsPlainText -Force

Import-Module ADDSDeployment
Install-ADDSForest `
-CreateDnsDelegation:$false `
-DatabasePath "C:\\Windows\\NTDS" `
-DomainMode "WinThreshold" `
-DomainName $domainName `
-DomainNetbiosName "EXAMPLE" `
-ForestMode "WinThreshold" `
-InstallDns:$true `
-LogPath "C:\\Windows\\NTDS" `
-SysvolPath "C:\\Windows\\SYSVOL" `
-SafeModeAdministratorPassword $safeModeAdministratorPassword `
-Force:$true

# Step 3: Configure NTP
w32tm /config /manualpeerlist:"time.nist.gov" /syncfromflags:manual /reliable:YES /update
Restart-Service w32time

# Step 4: Define and Implement AD Security Policies
# Define a strong password policy
$PasswordPolicy = @{
    Name = "StrongPasswordPolicy"
    Description = "Enforces password complexity and history."
}
$PasswordPolicyGPO = New-GPO @PasswordPolicy
Set-GPPermission -Name $PasswordPolicyGPO.Name -PermissionLevel GpoEdit -TargetName "Domain Admins"
New-GPLink -Name $PasswordPolicyGPO.Name -Target "DC=example,DC=com"

# Apply the password policy
Set-ADDefaultDomainPasswordPolicy -ComplexityEnabled $true -LockoutDuration "00:30:00" -LockoutObservationWindow "00:30:00" -LockoutThreshold 5 -MaxPasswordAge "42.00:00:00" -MinPasswordAge "1.00:00:00" -MinPasswordLength 12 -PasswordHistoryCount 24 -ReversibleEncryptionEnabled $false

# Step 5: Import the LDAP Server Authentication Certificate
# You must have your certificate ready at a known path
$certPath = "path\to\your\certificate.cer"
Import-Certificate -FilePath $certPath -CertStoreLocation Cert:\LocalMachine\My

# Step 6: Enable Secure LDAP (LDAPS)
Restart-Service NTDS -Force
# Confirm LDAPS is working, replace <YourDomainController> with actual domain controller name
Test-NetConnection -Port 636 -ComputerName <YourDomainController>

# End of script
```

## Disclaimer

The content of this guide is for informational purposes only. Implementation of the practices and scripts provided is at your own risk. While every attempt has been made to ensure the information is accurate, the author is not responsible for any errors, omissions, or damages arising from the use of this information.

## Conclusion

Setting up a secure Active Directory environment is a critical task that demands attention to detail and a focus on security best practices. Through these steps, we have laid a foundation for a domain that is not only functional but also resilient to various security threats. Remember, security is not a one-time effort; it's an ongoing process of monitoring, updating, and fortifying your systems against evolving threats.

Happy scripting, and stay secure!
