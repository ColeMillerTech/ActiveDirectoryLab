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
Launch the utility: <br/>
<img src="https://i.imgur.com/62TgaWL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Select the disk:  <br/>
<img src="https://i.imgur.com/tcTyMUE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Enter the number of passes: <br/>
<img src="https://i.imgur.com/nCIbXbg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Confirm your selection:  <br/>
<img src="https://i.imgur.com/cdFHBiU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Wait for process to complete (may take some time):  <br/>
<img src="https://i.imgur.com/JL945Ga.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Sanitization complete:  <br/>
<img src="https://i.imgur.com/K71yaM2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://i.imgur.com/AeZkvFQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
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
