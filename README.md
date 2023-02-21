<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

- Azure Virtual Machine
- osTicket Installation files
- Heidi SQL

<h2>Azure Installation Steps</h2>

<p>
</p>
<p>
We will be installing an open source help desk ticketing system called osTicket. In order to do so we are going to create a Virtual Machine (VM) in Microsoft Azure. We are using a VM in order to protect our physical machine just in case something breaks. 
<p>
<img src="https://i.imgur.com/5fpbKix.png" height="70%" width="60%" alt="Disk Sanitization Steps"/>
</p>
To create a VM in Azure first create a resource group and title it "osTicketVM". Next create a VM running on Windows 10 and tie it to the "osTicketVM" resource group. Select 4 vcpus for size, and create a username and password (Make sure to remeber it, you will need to log into it). Check the licensing box.  
<p>
<img src="https://i.imgur.com/zVETWK2.png" height="70%" width="60%" alt="Disk Sanitization Steps"/>
<p>
Continue to next page Networking. Allow Azure to create Virtual Network by default. 
<p>
<img src="https://i.imgur.com/PKxoamq.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
<p>
Next we will connect our VM using RDP. We will be using the public IPv4 address to add the VM to RDP. If you are a Mac user you will have to download Microsoft RDP. Login using the Username and Password create on Azure for the VM.

<h2>osTicket Installation Steps</h2>
<p>
</p>
<p>
<h4>Enable IIS in Windows with CGI</h4>

Once we have access to the VM we will have to enable IIS. 
</p> 
<img src="https://i.imgur.com/6qyabGo.png" height="70%" width="60%" alt="Disk Sanitization Steps"/>
</p> 
<br /> Simply access the control panel, then select Programs. Underneath Programs and Features select: Turn Windows features on or off. 
<br />In the popup menu expand Internet Information Services, then World Wide Web Services, then Application Development Features, Select: CGI. Apply changes by clicking ok. <br />Test if changes where made by opening a browser and typing in 127.0.0.1 which is a loopback. We are trying to load a webpage that is running off our computer
</p>  

<h4>Download and Install Additional Applications</h4>
<p>
Once we enabled IIS we will install a couple more applications that are needed to install osTicket. Files can be found here: https://drive.google.com/drive/u/1/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6

</p>
First we will download and install:
<p>
<br />PHP Manager for IIS
<br />Rewrite Module
<p>
Now we will create the directory C:\PHP
</p>
<p>
<img src="https://i.imgur.com/1sFsKsC.png" height="60%" width="45%" alt="Disk Sanitization Steps"/>
<p>
Create a new folder in C Drive and name it PHP
<p>
We have to download and install a couple more programs:
<p>
PHP 7.3.8 and unzip the contents into C:\PHP
<br />VC_redist.x86.exe
<br />Setup MySQL 5.5.62 as follows:
<br />--Typical Setup
<br />--Launch Configuration Wizard (after install)
<br />--Standard Configuration
<br />--Setup password you can remember; Username is root
</p>  

<h4>Installing osTicket</h4>
<p>
<img src="https://i.imgur.com/ShGZfCq.png" height="75%" width="65%" alt="Disk Sanitization Steps"/>
<p>
Now we will access the program Internet Information Services (IIS) as administrator. We will Register PHP from within the IIS. The php-cgi app can be found in Drive C. Restart Server once done. 
<p>
<img src="https://i.imgur.com/Q4vVkQ2.png" height="75%" width="70%" alt="Disk Sanitization Steps"/>
<p>
</p>
<p>
Next download osTicket. Then extract and copy the "upload" folder into c:\inetpub\wwwroot. Afterwards rename the folder to osTicket. 
</P>
<img src="https://i.imgur.com/KMn9YcT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
<p>
Open IIS Manager and restart the server. Once inside IIS manager go to Sites->Default Web Site->osTicket on the right, click "Browse*.80" from there your default browser should open osTicket webserver.
</p>
<img src="https://i.imgur.com/Yevfpxv.png" height="75%" width="65%" alt="Disk Sanitization Steps"/>
<br />
<p>
We will go back into IIS manager and enable some extensions. To do this we have to go to Sites->Default->osTicket
Then double click on PHP manager. Click on "Disable or enable an extension" Enable "php_imap.dll" & "php_intl.dll" & "php_opcache.dll" then refresh the osTicket webserver and obsereve the changes "Intl Extension" should now be enabled. 
</p>
<img src="https://i.imgur.com/8M20eqO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<p>
Go back into c:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php rename the file to c:\inetpub\wwwroot\osTicket\include\ost-config.php
Assign permissions to ost-config.php Disable inheritance->Remove all
New Permissions-> Type: Everyone-> Check Full control
</p>
<img src="https://i.imgur.com/RmVk3q5.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
<br />
<p>
Afterwards continue setting up osTicket in the browser (click continue) then you will name the Helpdesk to your liking. Select a default email that will receive emails from customers who submit tickets. 
</p>
<img src="https://i.imgur.com/C0q3lrr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<p>
We will have to Download and Install HeidiSQL
<br /> We will create a new connection Username: root Password: (Password you choose previously)
<br /> Next create a database. Right click Unnamed. Click Create New, then Database. Name it osTicket  
</p>
<img src="https://i.imgur.com/cBrVtyB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<p>
<br /> Continue Setting up osticket in the browser MySQL Database: osTicket MySQL Username: root MySQL Password: Password1 Click “Install Now!”
Congratulations, if there is no errors you will be taken to a the browser will say Congratulations!
Now time to clean up
Delete: C:\inetpub\wwwroot\osTicket\setup
Set Permissions to “Read” only: C:\inetpub\wwwroot\osTicket\include\ost-config.php
Login to the osTicket Admin Panel (http://localhost/osTicket/scp/login.php) using username and password
