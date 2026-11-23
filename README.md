# active-directory_dealing-with-account-lockouts_enabling-and-disabling-accounts_and-observing-logs
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory dealing with accounts in the Cloud (Azure)</h1>
This tutorial outlines how to deal with account lockouts, enabling and disabling accounts, and observing logs within Active Directory using virtual machines.<br />




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2025
- Windows 11
- Garuda Linux

<h2>Objectives</h2>

- Dealing with Account Lockouts
- Enabling and Disabling Accounts
- Observing Logs


<h2>Dealing with Account Lockouts</h2>

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
  From there I'll click the drop down menu of the following: 
</p>


