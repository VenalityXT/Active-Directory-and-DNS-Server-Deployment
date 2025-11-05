# **Active Directory & DNS Server Deployment on Windows Server 2022**

## **Project Overview**
This project demonstrates how to install, configure, and validate **Active Directory Domain Services (AD DS)** and **DNS Server** on a Windows Server 2022 virtual machine.  
The lab simulates a small enterprise domain environment, providing foundational experience in directory services, DNS name resolution, and domain management.

The process includes:
- Installing Active Directory Domain Services and DNS Server roles  
- Promoting the server to a domain controller  
- Creating a new forest and domain  
- Configuring static IP addressing  
- Verifying DNS resolution  
- Managing users and organizational units through Active Directory Users and Computers (ADUC)

---

## **Objective**
To deploy a functional **Active Directory domain controller** with integrated **DNS** on Windows Server 2022 and validate the environment through connectivity and name resolution testing.

---

## **Step 1: Open Server Manager**
After logging into Windows Server 2022, open **Server Manager**.  
From the **Dashboard**, select **“Add roles and features.”**

[Insert Image – Server Manager Dashboard]

This launches the **Add Roles and Features Wizard**, which is used to add or configure core Windows Server components.

---

## **Step 2: Select Installation Type**
Choose **“Role-based or feature-based installation.”**  
This option allows you to install AD DS and DNS roles directly onto this server.

[Insert Image – Installation Type Selection]

---

## **Step 3: Select the Destination Server**
Select **“This server from the server pool”** to apply changes locally.  
Your server should appear with its IP address and Windows version listed.

[Insert Image – Server Selection]

---

## **Step 4: Install AD DS and DNS Roles**
In the **Server Roles** list, check the boxes for:
- **Active Directory Domain Services**  
- **DNS Server**

You may see a validation message warning about the absence of a static IP address.  
AD DS and DNS require a fixed IP to prevent future connectivity issues.  
Continue to the next step to fix this.

[Insert Image – Validation Warning]

---

## **Step 5: Configure a Static IP Address**
Before continuing, open **Network Connections** → Right-click your Ethernet adapter → **Properties** → **Internet Protocol Version 4 (TCP/IPv4)** → **Properties**.  
Select **“Use the following IP address”** and configure it manually:
- **IP address:** 10.0.2.15  
- **Subnet mask:** 255.255.255.0  
- **Default gateway:** 10.0.2.15  
- **Preferred DNS server:** 10.0.2.15  
- **Alternate DNS server:** 8.8.8.8  

This ensures the server maintains a consistent network identity and can reliably act as its own DNS authority.

[Insert Image – IPv4 Static Configuration]

---

## **Step 6: Confirm Installation Selections**
On the **Confirmation** page, review your selected roles.  
Ensure both AD DS and DNS Server are listed, then click **Install**.  
Optionally, select **“Restart the destination server automatically if required.”**

[Insert Image – Installation Confirmation]

After installation, you’ll receive a post-deployment notification prompting to “Promote this server to a domain controller.”

---

## **Step 7: Promote the Server to a Domain Controller**
Select **“Promote this server to a domain controller.”**  
In the **Deployment Configuration** window, choose **“Add a new forest”** and specify the root domain name:

X
rapidascent.local
X

[Insert Image – Domain Configuration]

This creates a new Active Directory forest — a hierarchical structure that contains the domain and all its objects.

---

## **Step 8: Configure Domain Controller Options**
Keep default settings:
- **Forest functional level:** Windows Server 2016  
- **Domain functional level:** Windows Server 2016  
- **DNS Server** and **Global Catalog (GC)** checked  

Enter a **Directory Services Restore Mode (DSRM)** password.  
This is used for system recovery and should be securely stored.

[Insert Image – Domain Controller Options]

---

## **Step 9: Review Prerequisites**
Windows will perform a system validation before proceeding.  
Warnings about legacy cryptography or DNS delegation can be ignored in standalone lab setups.  
Once validation passes, click **Install** to promote the server.  
The system will automatically reboot when complete.

[Insert Image – Prerequisites Check]

---

## **Step 10: Verify AD DS and DNS Installation**
After reboot, return to **Server Manager → Manage → Add Roles and Features → Installed Roles**.  
You should now see:
- **Active Directory Domain Services**
- **DNS Server**

[Insert Image – Installed Roles]

Open **Active Directory Users and Computers (ADUC)** and **DNS Manager** to confirm both services are active.  
ADUC should show your domain (`rapidascent.local`) and DNS Manager should display matching forward lookup zones.

[Insert Image – ADUC and DNS Manager]

---

## **Step 11: Test Name Resolution**
Open PowerShell and test name resolution:
X
nslookup rapidascent.local
ping rapidascent.local
X

A successful lookup and reply confirm DNS and AD integration are functioning properly.

[Insert Image – nslookup and Ping Verification]

---

## **Step 12: Create an Organizational Unit (OU) and User**
In **Active Directory Users and Computers**:
1. Right-click your domain → **New → Organizational Unit** → Name it `IT_Department`.  
2. Inside the new OU, right-click → **New → User**.  
   - First Name: John  
   - Last Name: Doe  
   - User logon name: jdoe  
3. Assign a password and uncheck **“User must change password at next logon.”**

This demonstrates Active Directory object creation and management within an organizational structure.

[Insert Image – New OU and User Creation]  
[Insert Image – IT_Department OU with John Doe User]

---

## **Step 13: Review System Health**
Return to **Server Manager → Local Server → Events** and check for critical or warning messages.  
Kernel power messages are normal from reboots during role installation.  
If no persistent DNS or AD errors appear, the deployment is stable.

[Insert Image – Event Viewer Review]

---

## **Summary**
This lab successfully implemented a **domain controller** and **DNS infrastructure** using Windows Server 2022.  
Through this setup, the server now manages authentication, domain membership, and name resolution within the `rapidascent.local` forest.  

The configuration provides a foundation for adding domain-joined clients, managing user access, and applying Group Policy.  
By verifying DNS resolution, ADUC structure, and event logs, this lab confirms a complete and operational Active Directory environment suitable for future network simulations or SOC-related exercises.

---


---


<img width="1599" height="810" alt="image" src="https://github.com/user-attachments/assets/eea8cbc8-7126-472e-860a-195bf25cd0f4" />

<img width="784" height="558" alt="image" src="https://github.com/user-attachments/assets/60711616-ca8c-4121-9081-88f9c701ba0a" />

<img width="784" height="558" alt="image" src="https://github.com/user-attachments/assets/8114e281-6ea0-4d9f-9b13-f538603fed1e" />

<img width="782" height="558" alt="image" src="https://github.com/user-attachments/assets/7793abab-64fa-4b60-87c1-089168d7489b" />

<img width="1599" height="496" alt="image" src="https://github.com/user-attachments/assets/33a37032-1067-4172-b7fa-6d2ea2ca5343" />

<img width="1599" height="824" alt="image" src="https://github.com/user-attachments/assets/85349153-4645-41aa-9e83-85f3a460fd06" />

<img width="783" height="557" alt="image" src="https://github.com/user-attachments/assets/9b732ed2-2351-4ac0-b9ea-14c674c78914" />

<img width="1599" height="757" alt="image" src="https://github.com/user-attachments/assets/8ae39887-8e73-4334-91f5-5ad94dbf1d5b" />

<img width="758" height="558" alt="image" src="https://github.com/user-attachments/assets/73c924b9-0c6f-421a-9d1d-c4464cb94e97" />

<img width="759" height="557" alt="image" src="https://github.com/user-attachments/assets/4919770d-1db9-4d96-bfd5-b300b9ddd59b" />

<img width="758" height="557" alt="image" src="https://github.com/user-attachments/assets/bbd5e58c-7acf-4b2c-9866-c37d8e0b8212" />

<img width="1336" height="308" alt="image" src="https://github.com/user-attachments/assets/1c2aa41b-d9c9-455b-87ea-d6d239f011f6" />

<img width="964" height="525" alt="image" src="https://github.com/user-attachments/assets/d9c33b29-858d-48a1-b8a9-64a3d1c2ca4e" />

<img width="500" height="511" alt="image" src="https://github.com/user-attachments/assets/ac7e2759-7c1e-4728-a3d7-7e528b28b01f" />

<img width="570" height="528" alt="image" src="https://github.com/user-attachments/assets/2117a153-44da-4276-b013-8f370644a410" />

<img width="570" height="528" alt="image" src="https://github.com/user-attachments/assets/3f99e553-962f-4e87-bb7d-eaec0d1b4559" />

<img width="571" height="529" alt="image" src="https://github.com/user-attachments/assets/cf6a89fc-1b87-44cc-9ae4-2b4c0c486ee7" />

<img width="965" height="571" alt="image" src="https://github.com/user-attachments/assets/e63f9ea7-cd85-4833-abdd-b1cd2a6561d9" />

