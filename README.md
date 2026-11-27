
# active-directory_dealing-with-account-lockouts_enabling-and-disabling-accounts
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>


This tutorial outlines how to deal with account lockouts and enabling and disabling accounts within Active Directory using virtual machines.<br />




<h2>Environments and Technologies Used</h2>

- Garuda Linux (Linux is a free and open source operating software and there are different distributions of Linux, aka versions. Garuda is a distribution of Linux that I prefer to use)

  On my personal laptop, I'm using the operating software Garuda Linux. It's another operating system option to use besides Windows or MacOs. On Linux, one of the main ways to use Remote Desktop is to use an application called Remmina. For example, if you're trying to connect to a Windows computer, once you open the app, there'll be a plus sign at the top of the app screen. You click that to add a new connection profile. From there, next to protocol, there'll be a drop down menu and you choose "RDP: Remote Desktop Protocol" which is specifically for connecting to Windows computers. From there, you just need the public IP address, username, and password of the computer you're trying to connect to and enter those in the corresponding fields on the Remmina screen. Once entered, you just click the Connect button and a screen should pop up displaying the screen of the computer you're connected to. 
- Microsoft Azure

  
  Microsoft Azure is Microsoft's cloud computing platform. It lets businesses, developers, and individuals use Microsoft's internet-based computing services instead of having to buy and maintain their own physical servers and IT infrastructure.

Think of Azure as renting computers, storage, databases, and software over the internet from Microsoft.
- Virtual Machines
  
  A virtual machine is basically a computer that is not physically there with you, but you're able to still access it remotely.

I'll be using two virtual machines running in Microsoft Azure, worth noting that both virtual machines ARE ON THE SAME VIRTUAL NETWORK within Azure. I've done this to simulate a business environment where there could be hundreds or even thousands of computers on the same business network: One I have named (dc-1) and the other is (client-1). I'll access these virtual machines with remote desktop, which is basically a way to access computers even though you're not physically there with them.

-DC-1 is a server (a server is basically a computer that serves other computers) and is using the operating software Windows Server, and Active Directory will be running on this server. DC-1 will be the domain controller in this example. 

A domain controller is a server that manages and controls access to computers, users, and resources within a Windows network. It basically acts as the central authority for authentication, authorization, and security in an organization/business. I like to think of a domain controller as a security guard for a company's network: it checks who you are, verifies your credentials/login info, and decides what you're allowed access to. 

-Client-1 is a virtual machine that is running on the operating software Windows 11. You can think of this virtual machine as just a regular old computer. 


- Remote Desktop
  
  Remote Desktop is a technology that allows you to access and control another computer from a different location using the internet or a network.

Basically, it's like sitting in front of another computer even though you're physically somewhere else.

- Active Directory Domain Services
  
  Active Directory is Microsoft's directory service that stores and organizes information about users, computers, groups, and network resources.

   In this example, there are over 1,000 user accounts that Active Directory has in the domain. The virtual machine, Client-1, is part of that domain. 
  
- PowerShell
  
  Basically, PowerShell lets you tell a computer what to do by typing instructions in to a command line, instead of having to click through menus. 

<h2>Operating Systems Used </h2>

- Windows Server 2025
- Windows 11
- Garuda Linux (Linux is a free and open source operating software and there are different distributions of Linux, aka versions. Garuda is a distribution of Linux that I prefer to use)

<h2>Objectives</h2>

- Dealing with Account Lockouts
- Enabling and Disabling Accounts



<h2>Dealing with Account Lockouts</h2>

<p>
  <img width="1580" height="822" alt="logging-in-to-microsoft-azure" src="https://github.com/user-attachments/assets/9abdecd4-a79e-4413-a540-d309c047d940" />

</p>

<p>
  First, I'm going to login in to Microsoft Azure. This is the first screen I see after logging in. From here, near the top of the screen where it says "Azure Services" it says "Virtual Machines". I'll click that to go to the virtual machines that I have already created beforehand. 
</p>

<p>
  <img width="1596" height="754" alt="public-ip-address-of-dc-1-highlighted" src="https://github.com/user-attachments/assets/89f55992-5631-42e3-8c69-e6b1f29eaa5c" />

</p>

<p>
  First, I want to use Remote Desktop to connect to the virtual machine (dc-1) which is the domain controller in this example. This has been explained above in the "Environments and Technologies" section. For this I want to take note of the public IP address which has been highlighted in this screenshot. I'll also need the username and password of this virtual machine which I won't show for security purposes. Once I have those I'll open up "Remmina" the remote desktop application on Garuda Linux which allows you to connect to other computers remotely. 
</p>

<p>
<img width="1504" height="856" alt="right-click-start-in-dc1-vm" src="https://github.com/user-attachments/assets/0984ded7-9c19-4dcc-a2d2-3216ebb23e36" />

</p>
<p>
First, I want to configure Account Lockout settings. So I want to head to the Group Policy Management Console (GPMC). I will right click start on the home button. Then I will click run.
</p>
<br />

<p>
  <img width="1516" height="823" alt="gpmc msc-in -the-run-option" src="https://github.com/user-attachments/assets/f49bc8b2-ba79-4b3f-b0aa-f15344582089" />

</p>

<p>
  After that I will type "gpmc.msc" , then click "OK".

  <p>
    
  </p>
</p>


</p>
<br />

<p>
  <img width="1511" height="842" alt="right-click-default-domain-policy" src="https://github.com/user-attachments/assets/6c146abe-dd20-48ce-908d-aaa60ccfd54f" />

</p>

<p>
  After that, I will right click on "Default Domain Policy" and then I will click "Edit".
</p>

<p>
  <img width="1516" height="855" alt="heading-to-account-lockout-policy" src="https://github.com/user-attachments/assets/84ead0df-9721-4d23-be16-bf5ad3e73a6f" />

</p>

<p>
  From there I'll click the drop down menu of the following: Policies-> Windows Settings-> Security Settings-> Account Policies-> Account Lockout Policy. I'll click "Account Policy". 

  After that, I'll click "Account Lockout Duration" and set it to 10 minutes. This is basically once password attempts have failed the person won't be able to retry entering a password for 10 minutes.
</p>

<p>
  <img width="1512" height="855" alt="setting-account-lockout-duration" src="https://github.com/user-attachments/assets/08209985-462d-410f-98c7-f36ae660437b" />

</p>

<p>
  Here, I'm setting the account lockout duration for 10 minutes. I'll click "Apply" then "OK".
</p>

<p>
  <img width="1513" height="856" alt="account-lockout-duration-set-to-10-minutes" src="https://github.com/user-attachments/assets/b51412dd-3ff1-448a-9436-67ab40437dcb" />

</p>

<p>
  Under "Account Lockout Duration" there's "Account Lockout Threshold". The account lockout threshold automatically got set to 5 password attempts once I set the account lockout duration. I'll leave as is. This is basically saying a person has 5 attempts to type in the password correctly before being locked out.
</p>

<p>
  <img width="1516" height="850" alt="allow-admin-account-to-unlock-account" src="https://github.com/user-attachments/assets/ed576d69-4a3c-4fe6-b35e-fcb133ac51c1" />

</p>

<p>
  Here I'm making sure that an admin account will be able to unlock accounts that have been locked. I click "Allow Administrator account lockout", then in the pop-up I click "Define this policy setting" and check "Enabled". After that click "Apply" then "OK".
</p>

<p>
  <img width="1525" height="848" alt="force-computers-to-accept-policy" src="https://github.com/user-attachments/assets/bcd6529b-8840-4622-b92c-6052ebd4ac38" />

</p>

<p>
  After that, I'll log in to another virtual machine as an admin. From there I'll open the command line. I'll type "gpupdate /force" then hit enter. This will cause the changes I've made to be updated to the system.
</p>

<p>
  <img width="1528" height="484" alt="pt2-failing-to-login-5-times" src="https://github.com/user-attachments/assets/e40dc58c-be84-4c79-bfa0-9453127f6ea2" />

</p>

<p>
  Now I'll be trying to log in as a User with an incorrect password 5 times in a row. The name of the user is "wuta.neg". After the fifth incorrect attempt, the account should be locked out.
</p>

<p>
  <img width="1527" height="191" alt="account-has-been-locked-out" src="https://github.com/user-attachments/assets/e7a8e0cf-c05a-4910-8025-0af3138a632e" />

</p>

<p>
  The account has been locked out. Now as an admin user I'll unlock the account.
</p>

<p>
  <img width="1216" height="610" alt="right-click-on-account-then-click-properties" src="https://github.com/user-attachments/assets/9745e74c-a54d-4e21-902c-3d3ab5b32c5d" />

</p>

<p>
  Now I've logged in as "jane_admin". I've opened up "Acitive Directory: Users and Computers". I've right clicked "mydomain.com" in the menu and clicked "Find". In the pop up window, next to "name" I'ved typed in the account name that has been locked out. From there there, towards the bottom, the name of the account is listed. I right click the account name, then click "Properties".
</p>

<p>
  <img width="1236" height="700" alt="check-unlock-account-then-click-apply" src="https://github.com/user-attachments/assets/21d5bffe-db9a-48bc-8f80-22a8e879110d" />

</p>

<p>
  From there I check the box that says "Unlock Account" then click "Apply" then "OK". The account should be unlocked, I will try to log back in as the User that was locked out.
</p>

<p>
  <img width="1001" height="661" alt="retry-to-login-after-account-unlocked" src="https://github.com/user-attachments/assets/0a9907ef-65b7-40ea-9e9c-12475516e768" />

</p>

<p>
  Here I'm back at the login screen and will attempt to login with the correct password.
</p>

<p>
  <img width="881" height="285" alt="account-unlocked-successful" src="https://github.com/user-attachments/assets/6b41a9ed-5348-4ea9-a017-b66b69194a49" />

</p>

<p>
  The account has been successfully unlocked!
</p>

<h2>
  Disabling and Enabling Accounts
</h2>

<p>
  For this portion, I'll use the same user account "wuta.neg".
</p>

<p>
  <img width="1216" height="610" alt="right-click-on-account-then-click-properties" src="https://github.com/user-attachments/assets/69e73309-02ca-4071-b064-bcfdb6007744" />

</p>

<p>
  For this, I'm logged in as an admin account. In the Windows 11 search bar, I go to "Active Directory: Users and Computers". Then I right click "mydomain.com", then click "Find". From there I type in the user account name and click "Find Now". Then the name appears down below, and I right click on the account "wuta.neg". From there I click "disable account".
</p>

<p>
  <img width="632" height="552" alt="account-disabled" src="https://github.com/user-attachments/assets/e6f9f863-ffd1-4af0-ad37-e29d2e8fb949" />

</p>

<p>
  "wuta.neg" has been disabled. I will attempt to log in to this account now.
</p>

<p>
  <img width="1537" height="148" alt="wuta neg-has-been-disabled" src="https://github.com/user-attachments/assets/00d149d2-7357-4d5a-96fb-22539d2a1c20" />

</p>

<p>
  I'm not able to log in since the account has been disabled. I will now re-enable the account and attempt to log in afterwords.
</p>

<p>
  <img width="1059" height="648" alt="enable-account-again" src="https://github.com/user-attachments/assets/0811797c-9064-4509-986b-ee9717a1ae0e" />

</p>

<p>
  From here I'm logged back in as an admin account. I will open up "Active Directory: Users and Computers" and right click "mydomain.com" and find the account "wuta.neg". Then I will right click the account and click "Enable Account". 
</p>

<p>
  <img width="666" height="564" alt="wuta neg-enabled" src="https://github.com/user-attachments/assets/086fa97e-e70f-487b-9c67-e131a8024883" />

</p>

<p>
  Now I will attempt to log in as the account "wuta.neg"
</p>

<p>
  <img width="867" height="638" alt="Screenshot_20261122_220505" src="https://github.com/user-attachments/assets/2e30eb8a-3583-463a-b7fb-31c6d8d9f4de" />

</p>

<p>
  Here, I'm back at the login screen and will attempt to login.
</p>

<p>
  <img width="881" height="285" alt="account-unlocked-successful" src="https://github.com/user-attachments/assets/83753034-1712-4068-a087-ec3989fee400" />

</p>

<p>
  Mission success! The account has been re-enabled and I was able to log back in!
</p>



