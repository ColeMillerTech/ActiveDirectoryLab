<h1>Active Directory Home Lab</h1>


<h2>Description</h2>
In this lab, I utilize Oracle VM VirtualBox to establish a Windows 2019 Server Virtual Machine (acting as the controller) and implement Active Directory. Concurrently, I create a Windows 10 virtual machine (serving as the client) and interconnect the two via an internal network. Following the configuration of both the controller and client VMs, I employ a PowerShell script to seamlessly generate 1000 user accounts within the Active Directory.<br />


<h2>Languages and Software Used</h2>

- <b>PowerShell</b> 
- <b>[Oracle VM VirtualBox](https://www.virtualbox.org/wiki/Downloads)</b>

<h2>Environments Used </h2>

- <b>[Windows 10](https://www.microsoft.com/en-us/software-download/windows10)</b>
- <b>[Windows Server 2019](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2019)</b>

<h2>Lab Walkthrough:</h2>

<p align="center">
<h3>Creating our Windows Server 2019 Virtual Machine</h3>
Initiate the creation of a new virtual machine by selecting "New" within VirtualBox. Assign the name "Server (Domain Controller)" to the VM and designate the "Windows Server 2019" ISO file as the boot.
<br />
<br />
<img src="https://i.imgur.com/j4IdxLn.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Adjust the allocated RAM for the VM according to your system specifications. For instance, in this project conducted on a spare laptop with limited RAM, 2GB was allocated to the VM. However, if your system permits, consider assigning a larger amount of RAM to enhance performance.  <br/>
<br />
<img src="https://i.imgur.com/NLwWnJT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Choose the version of Windows Server 2019 that includes the "Desktop Experience" option. This version provides a graphical user interface (GUI) rather than just a command line interface, making it more user-friendly and suitable for most scenarios. <br/>
 <br />
<img src="https://i.imgur.com/wZwXmVS.png" height="80%" width="80%"/>
<br />
<img src="https://i.imgur.com/t6bs31H.png" height="80%" width="80%"/>
<br />
<br />
<h3>Configuring Active Directory</h3>
Now that our Server is all loaded up, I'll install Active Directory.
<br/>
<br />
<img src="https://i.imgur.com/C6crcne.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Let's proceed with establishing a new forest domain for our Active Directory. This domain will serve as the primary authentication environment for all users to log into.
<br />
<br />
<img src="https://i.imgur.com/AMkrDNE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<h3>Testing Active Directory</h3>
Now that we have our new domain "coledomain.com," let's proceed to create a new user group called "ADMIN" and add a user to it. Once the user is created, I'll log out of the server account and verify that I can successfully log into the new Admin Account.   <br/>
 <br />
<img src="https://i.imgur.com/HslJb7m.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/KhVq3Op.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/ya02rfZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
Success! I was able to log into the new Admin account no problem!
<br />
<br />
<h3>Using Powershell to create 1000 User Accounts</h3> 
<br/>
<br/>
Names.txt file with over 1000 Randomly generated names which will be used in the user creation powershell script (1_CREATE_USERS.ps1)
<br/>
<img src="https://i.imgur.com/n6yoMhm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
Time to run the script. By default Windows won't allow us to execute unknown scripts from the internet, so we need to enable execution of our script by running the following command:
<br/>
<br/>
Set-ExecutionPolicy Unrestricted
<br/>
<br/>
Powershell user creation script:
<br/> 
 
```
# ----- Edit these Variables for your own Use Case ----- #
$PASSWORD_FOR_USERS   = "Password1"
$USER_FIRST_LAST_LIST = Get-Content .\users.txt
# ------------------------------------------------------ #

$password = ConvertTo-SecureString $PASSWORD_FOR_USERS -AsPlainText -Force
New-ADOrganizationalUnit -Name CREATED_USERS -ProtectedFromAccidentalDeletion $false

foreach ($n in $USER_FIRST_LAST_LIST) {
    $first = $n.Split(" ")[0].ToLower()
    $last = $n.Split(" ")[1].ToLower()
    $username = "$($first.Substring(0,1))$($last)".ToLower()
    Write-Host "Creating user: $($username)" -BackgroundColor Black -ForegroundColor Cyan
    
    New-AdUser -AccountPassword $password `
               -GivenName $first `
               -Surname $last `
               -DisplayName $username `
               -Description 'Created via a Script' `
               -Name $username `
               -EmployeeID $username `
               -PasswordNeverExpires $true `
               -Path "ou=CREATED_USERS,$(([ADSI]`"").distinguishedName)" `
               -Enabled $true
}
```

<img src="https://i.imgur.com/oKlKYFo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<h3>Success!</h3>
As you can see 1000 User Accounts created!
<br/>
<br />
<img src="https://i.imgur.com/8HnY2JM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
