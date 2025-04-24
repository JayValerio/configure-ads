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

<h2>
  Join Client-1 to your domain (mydomain.com)
</h2>

<p>
  
  ![image](https://github.com/user-attachments/assets/d4eaae81-bcab-4173-8e7a-e5f79b212235)

</p>
<p>
  Now that we've set up the Admin, lets set up our user Client-1 computer and add them to the domain. </br>
  To do this we right click start, System, Rename this PC (advanced), Computer Name, Change. </br>
  In the Member of section click the 'Domain' box and in the empty field type in the domain controller, in this case 'alphadomain.com'. </br>
  A window will pop up for you to log into the domain, do so as the admin. Once logged in it will prompt you to restart, restart your RDC.
</p>


<p>
  
  ![image](https://github.com/user-attachments/assets/d7eaa557-87a0-4c47-823a-96e5150fb196)

</p>

<p>
  To verify that the computer was added to the domain, go back to the Domain Controller.</br>
  In Active Directory Users and Computers click your domain, for this example thats 'alphadomain.com', select computers and you should see your client-1 there.
</p>

<h2>
  Setup Remote Desktop for non-administrative users on Client-1
</h2>
<p>
  Here we will configure Client-1 to allow RDC from non-administrative users.
</p>
<p>
  
  ![image](https://github.com/user-attachments/assets/80fc6526-a712-465b-94a4-d85e29f958b8)

</p>
<p>
  First, right click the start icon on the botton right, go to system, Remote desktop.
</p>

<p>
  
  ![image](https://github.com/user-attachments/assets/a901784b-4249-4160-9d85-69aa0804e518)

</p>
<p>
  Next, click 'Select users that can remotely access this PC' under User accounts.</br>
  In the pop up widnow select 'Add...'
</p>

<p>
  
  ![image](https://github.com/user-attachments/assets/af0148cc-654d-49db-b690-0742ac6eabcb)

</p>

<p>
  In this window type in 'domain users', then check names, then add the domain users by pressing 'OK'. This will allow any user in the domain to access the Client-1 desktop remotely.
</p>

<h2>
  Create a bunch of additional users and attempt to log into client-1 with one of the users
</h2>

<p>
  We will now create several users with PowerShell. This will allow us to pick one at random and use that account to log into client-1.
</p>

<p>
  
  ![image](https://github.com/user-attachments/assets/60aa2e53-2d9c-44e8-bdec-87d4ded6f14a)

</p>
<p>
  First we log into DC-1 as our Admin, Jane. We open powershell ISE as an administrator.
</p>
<P>
  
  ![image](https://github.com/user-attachments/assets/22d3b1e4-9367-4d28-a9de-b3d6ff2b04a1)

</P>
<p>
  next we create a new file in powershell, save that file as "create new users" or whatever you prefer. Run this script: https://github.com/JayValerio/Create-10k-pwrshell. Click run and wait for the users to be created.
</p>
<p>
  
  ![image](https://github.com/user-attachments/assets/bd2f9311-1204-4d22-9309-52e214619e1b)

![image](https://github.com/user-attachments/assets/2d3e1e2b-1834-4ebc-9459-ec0418a47196)

</p>

<p>
  Once this is completed open 'Active Directory Users and Computers', go to the OU '_EMPLOYESS' and check that all users have been added to this folder. All users that we have created will have 'Password1' as the password. We can now pick one at random to log into Client-1.
</p>
<p>
  
  ![image](https://github.com/user-attachments/assets/60b1248a-c174-455c-9a59-deb6755e5a5e)

</p>
<p>
  For this example 'com.lok' will be our random picked user.
</p>
<p>
  
  ![image](https://github.com/user-attachments/assets/02345225-4c08-4687-b6be-50a700a4e584)

  ![image](https://github.com/user-attachments/assets/f287602a-b4fb-4293-8edd-4f4056a464d5)


</p>
<p>
  As you can see now we can log into client-1 with any of the 10000 users we have in ADCU(Active Directory Users and Computers). Next we will look into how to manage each individual account and group policy.
</p>
<h2>
  Dealing with Account Lockouts
</h2>


<p>
  
  ![image](https://github.com/user-attachments/assets/331494e6-7eb9-4ae9-8b70-604fc6bc40a2)


</p>
<p>
  We will configure the account lockout policy in group policy management tab on DC-1. right Click start, then Run, type in 'gpmc.msc' 
</p>

<p>
  
 ![image](https://github.com/user-attachments/assets/15084c49-38f6-412e-a3b1-066719a443df)
![image](https://github.com/user-attachments/assets/5d53a91f-4bc1-4740-a915-4931c3700031)


</p>
<p>
  Next we find our 'Default Domain Policy' and right click, edit, Policies, Windows Settings, Security Settings, Account Policies, Account Lockout Policy. </br>
  </br>

  Account Lockout duration: How long is the acocunt locked out. </br>
  Account Lockout threshold: How many attempts does the user get before being locked out. </br>
</br>

<p>
  We can use these two setting to control how long someone is locked out of the account and how many attempts they receive before getting locked out.
</p>

![image](https://github.com/user-attachments/assets/4d2a1a7b-c6ea-4335-9cfc-6d5b635d4de5)

</p>
<p>
  Now that the new policy has been added we can either wait about  90 minutes for the policy to refresh or we can force the refresh to client-1 by pushing a command prompt.</br>
  To do this we simply log into 'jane_admin' on client-1.
  </p>
<p>
  
  ![image](https://github.com/user-attachments/assets/8f08d143-e32f-4e59-8e93-e87cfc6bd3e8)
![image](https://github.com/user-attachments/assets/1cf055af-ab7e-4cbf-8b4e-4f800b571be1)
![image](https://github.com/user-attachments/assets/c838ec53-a6cb-4883-9628-2ed617954f5e)

</p>
<p>
  Open up 'command prompt' once logged in as your admin on client-1. type in the command 'gpupdate /force' and this will force the computer policy to update immediately. You can verify that the group policy updated by running command line as an admin and running the command 'gpresult /r' this will show you which GP was last updated and when it happened.
</p>












<p>
  
  ![image](https://github.com/user-attachments/assets/48280fc8-e0a3-4834-b5c5-fecfe6a4b693)
![image](https://github.com/user-attachments/assets/1cbdb568-09a1-48a9-92a2-a967a357d661)

</p>
<p>
to demonstrate an account lock out we will attempt to log into one of the users but purposely fail 5+ times to lock ourselves out.
  
</p>

<p>
  
  
![image](https://github.com/user-attachments/assets/75b87a3a-8dcd-4b2f-9cb9-a41d2bd30492)

</p>
<p>
  Now that the account is locked out, we can go back into DC-1 and unlock the account to gain access to it. First we right click our domain 'alphadomain.com\' and select find. Then we type in our account we want to work on in this case that is 'com.lok'.
</p>
<p>
  
 
![image](https://github.com/user-attachments/assets/0a914305-3580-49b1-bbc0-a36f996cbae3)

</p>
<p>
  now that we have the account, right click it and select properties. go to 'Account' and check the box 'Unlock account. This account is currently locked...' then hit apply and try to log in again with the acocunt.
</p>
<p>
  
  ![image](https://github.com/user-attachments/assets/9025b9d0-69c1-45ea-962a-d1ef41ecaa78)

</p>
<p>
  Now that we reset the account, we can access it again. This can be used with any of the accounts created on the domain unlock them if ever needed.
</p>
<p>

  ![image](https://github.com/user-attachments/assets/32877cd3-ba1c-49cb-bad1-57aeccf32c6e)
  
</p>
<p>
  In the case where you need to reset the password there is an option to do so right when you look up the account. Once you right click the account you are looking for, simply hit 'Reset Passowrd...' you can set the new password and unlock the users account from here as well.
</p>

<h2>
  Dealing with Account Lockouts
</h2>

<p>
  For this example we will be disabling our 'com.lok' account
</p>

<p>
  
  ![image](https://github.com/user-attachments/assets/4c24aa73-57ad-4d34-b13e-f10f2f48956e)

</p>

<p>
  As you can see when we attempt to log in the account has been disabled.
</p>

<p>
 
  ![image](https://github.com/user-attachments/assets/942f0d28-8257-42c9-b76b-041b293a23f8)
![image](https://github.com/user-attachments/assets/10f38d10-1baf-471f-82ff-b41fdf50b44f)

</p>
<p>
  Back in DC-1 we search up the user in ADUC, right click the account and enable the account. Now we can log in.
</p>

<h2>
  Observing Logs
</h2>
<p>
We can observe logs on any machine by simply clicking start and typing in 'eventvwr.msc'.
</p>
<p>
  
  ![image](https://github.com/user-attachments/assets/bd731f8c-3356-45ff-b40f-26f344b3e66e)

</p>
<p>
  In DC-1 we pulled up the event viewer where you can see all those authentication logs.
</p>
<p>
  
  ![image](https://github.com/user-attachments/assets/2381ef5a-ab1e-47b3-b394-ec1f660098d9)

</p>
<p>
  In the event viewer you open 'Windows Logs' then right click 'Security' and select 'Find...'. here we can look for the recent account we used 'com.lok'
</p>
<p>
  
  ![image](https://github.com/user-attachments/assets/e6785e18-ee47-4bb2-be74-5036c015916a)

</p>
<p>
  Here we can see all the activity for 'com.lok', from the account logging in/out, the account being disabled/Enabled, the lockouts and everything in between. If you check the event logs on the computer that the account was last used on, you will see a much more detailed list of events.
</p>
<br />





















