# configure-nfs-permissions

![images](https://github.com/user-attachments/assets/225e344e-ac25-433e-9068-17918bf6c620)


<h1>Network File Shares and Permissions Deployed on Virtual Machines (Azure)</h1>
This exercise outlines the implementation of NFS and Permissions within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines)
- Remote Desktop
- Active Directory Domain Services
- NFS and Permissions

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)


<h2>Deployment and Configuration Steps</h2>
<p>
First, I reset one of the Users passwords in order to log in to our Client Virtual machine with their account.
</p>

![(1) Using DC VM to reset user password to log into client VM](https://github.com/user-attachments/assets/237918a3-3b99-41a2-8efe-9baee23ca107)

<br />
<p> Next, I will be creating read-access, write-access, no-access, and accounting folders on the C:\ drive of our Domain Controller VM.</p>


![(2) Create access and accounting folders on the C drive on DC VM](https://github.com/user-attachments/assets/43620b88-f90f-49aa-a35a-ac36da2f66e5)

<p>
After creating the access and accounting folders, I edited the permissions of each folder and assigned them to Groups created in the Active Directory. The "Domain Users" group were given permissions to only the "read-access" and "write-access" folders. The "Domain Admins" group was given permissions to the "no-access" folder.
</p>

![(3) give read permissions to Domain users](https://github.com/user-attachments/assets/476e51b9-1778-4679-a487-765659100181)
![(5) give read and write permissions to domain users](https://github.com/user-attachments/assets/b6bbdc67-ff0b-464d-b94a-c870fa51aa66)
![(6) give read and write permissions to Domain Admins](https://github.com/user-attachments/assets/0d7d648e-0ecb-484c-ac3c-c8b6a7ac8002)

<br />

<p>
After setting up the permissions on each folder I attempted to access the folders as a Client who is a part of the Domain Users group on the Client VM. They are able to access the "read-access" and "write-access" folders, since they have permissions to do so as a part of the Domain Users group. However, they are unable to access the "no-access" folder as it is only available to the Domain Admins.
</p>

![(7) Attempt to access newly created files as a Client](https://github.com/user-attachments/assets/dc532c54-cb19-457a-b3f9-e38111ca7ffa)
![(9) showing access to read access folder as client](https://github.com/user-attachments/assets/7030d7c3-e2b8-4ec1-b326-8fc4fc5306e0)
![(10) showing access to write access folder as client](https://github.com/user-attachments/assets/c9f9eb81-b5b6-4508-a12c-501cf3b7e5fd)
![(8) showing no access to folder with Admin only permissions as client](https://github.com/user-attachments/assets/d0f86b23-84f5-4ed1-aacf-34e581500ad3)

<br />

<p>
After checking their access, I created a Security Group named "ACCOUNTANTS" in the Active Directory. Next, I edited the accountants folder to give the ACCOUNTANTS group read/write permissions. 
</p>

![(11) creating new security group ACCOUNTANTS on DC VM](https://github.com/user-attachments/assets/c19802a8-2408-48be-a32e-3b7df286c0ad)
![(12) giving accounting folder read write permissions to new ACCOUNTANTS group](https://github.com/user-attachments/assets/ff6dc53a-978a-42b2-810e-9a47e1ba3b4d)

<br />

<p>
Finally, I attempted to access the accounting folder as a user without permissions, then I gave the user permissions by adding them to the ACCOUNTANTS security group in the Active Directory. After doing so, the use now has access to the accounting folder.
</p>

![(13) attempt access to accounting folder as user without permissions](https://github.com/user-attachments/assets/f1a1b3ff-abf9-416b-8023-a8b41a662b5f)
![(15) make new user part of the ACCOUNTANTS security group 2](https://github.com/user-attachments/assets/e2d323fd-9505-42f6-b9ed-90bf97b50ac1)
![(16) new user now has access to accounting folder](https://github.com/user-attachments/assets/ecc2b648-d427-42b8-81fd-88f41cff8bff)



