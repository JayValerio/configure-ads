<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell
- Active Directory

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)
<h2>Objectives </h2>

- Install Active Directory
- Create a Domain Admin user within the domain
- Join Client-1 to your domain (mydomain.com)
- Setup Remote Desktop for non-administrative users on Client-1
- Create additional users and attempt to log into client-1 with one of the users

<h2>Install Active Directory</h2>

<p>
First we will set up our DC-1 VM as our Domain Controller and install active directory in it.
</p>

<p>
  
  ****![image](https://github.com/user-attachments/assets/e4fb3d13-bfdd-4d46-bc8e-0c773341c25d)

</p>

First select 'Add Roles and Features', hit next until you get to where it asks you to select roles.
<p>
  
  ![image](https://github.com/user-attachments/assets/2ac5ae72-4d79-428b-9392-9fea7957808e)

</p>
  <p>

![image](https://github.com/user-attachments/assets/d068f76f-cee5-4cca-b0fd-94858ee4ab22)


    
  </p>

<p>
  
  ![image](https://github.com/user-attachments/assets/e113dbb9-78ef-4ef4-993e-7189a6c033ae)

</p>

<p>

![image](https://github.com/user-attachments/assets/f77a3708-9dfe-4a16-8e6f-a89fc3d1968e)

  
</p>
<p>
  Here you select 'Active Directory Domain Services' select 'Add Features' and hit next until you reach the end.
</p>
<p>

  ![image](https://github.com/user-attachments/assets/69f0951d-f491-462a-aef3-de7961c78007)

</p>

<p>
  From here select restart if required and install all the new features.
</p>

<p>
  Once all Features are installed we will promote DC-1 to operate as a Domain Controller by setting up a forest as alphadomain.com
</p>

<P>
  
  ![image](https://github.com/user-attachments/assets/85b1a2ff-de8e-4c5a-a51a-3863c9ab7090)

</P>

<P>
  From here we can 'Promote this server to a domain controller'
</P>
<p>
  
  ![image](https://github.com/user-attachments/assets/78f0ef6c-f36d-41ba-8ceb-a156516f51a5)

</p>
<p>
  on this window select 'add a new forest' then set the root domain, in this case it would be 'alphadomain.com'. hit next.
</p>

<p>
  
  ![image](https://github.com/user-attachments/assets/2b7216e2-b388-4296-9916-7fb9f9494627)

</p>
<p>
  Here set the password for DSRM (Directory Services Restore Mode) and hit next
</p>
<p>
  
  ![image](https://github.com/user-attachments/assets/103ff228-5fd0-40e6-b331-6bb476eebd2a)

</p>
<p>
  Uncheck create DNS delegation. Hit next until you reach the installation window and install the program. your system will reboot after the installation is complete.
</p>
<p>
  
  ![image](https://github.com/user-attachments/assets/3652e305-d130-4a35-a7db-dd719aa6194b)

</p>

<h2>
  Create a Domain Admin user within the domain
</h2>
<p>
  First open up active directory users and computers.
</p>
<p>

  ![image](https://github.com/user-attachments/assets/eed7dbf6-8e0d-4001-8f71-a0a88b4f24e1)

</p>
<p>
  Next we create 2 Organizational Units (OU) </br>
  1. _EMPLOYEES</br>
  2. _AADMINS
</p>
<p>

![image](https://github.com/user-attachments/assets/e05b5649-a073-4b1d-b319-b366caf9f64c)

</p>
<p>
  Right click 'alphadomain.com', click new then Organizational Unit and create each Unit.
</p>
<p>

![image](https://github.com/user-attachments/assets/8e3eb346-6335-4722-aaf8-d5738ef63fb6)

  
  ![image](https://github.com/user-attachments/assets/2f7b5d70-796c-44d4-9a97-d4571df83a54)
</p>
<p>
next we create a new user in the admin folder. In this case  'jane_admin' will be our new user.
</p>
<p>

![image](https://github.com/user-attachments/assets/dc5f43a7-cd5f-4ae1-9a47-5e2a65afb621)

</p>
<p>
  This account is still not an admin, in order to do this we will add the account to the built in admins security group.</br>
  In the admins folder, right click the account you want as an admin and go to properties, Member Of, Add - "Domain Admin", Check names </br>
  then add the built in domain group.
</p>
<p>
  
  ![image](https://github.com/user-attachments/assets/349d23f0-3dbe-4ee6-ace8-e8908254d62e)

</p>
<p>
  Now we will log into DC-1 as our 'jane_admin' account.
</p>

<p>
  
  ![image](https://github.com/user-attachments/assets/d4eaae81-bcab-4173-8e7a-e5f79b212235)

</p>
<p>
  Now that we've set up the Admin, lets set up our user Client one and add them to the domain. </br>
  To do this we right click start, System, Remane this PC (advanced), Computer Name, Change. </br>
  In the Member of section click the 'Domain' box and in the empty field type in the domain controller, in this case 'alphadomain.comj'
</p>












<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
