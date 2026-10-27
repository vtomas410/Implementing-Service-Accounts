# Implementing Service Accounts | Single Purpose Computers

**Objectives:**

- Gain practical experience with AD Service Accounts.
- Practice setting up and managing a single computer with a service account and special configurations.
- Use Sysinternals tools to setup and manage computers.

---

**What is a Service Account?**

A user account is created for a person to log into a computer, access files, and use applications. A service account is created for an application, Windows service, or automated task to perform specific functions. Service accounts allow programs to run automatically without requiring a person to log in. For example, a service account can run nightly backups or allow an application to access a database. Unlike regular user accounts, service accounts are designed for non-human use. They should have only the permissions necessary to perform their assigned tasks to reduce security risks.

For this Homelab we will create a computer that will display a program 24/7. It will be logged in with a service account and does not require a human to type anything in. It is used for display usually. 

Example: Kiosk, Screens at resturants

---

**Prerequisites:**

- Windows Server (VM)
- Active Directory Domain Services
- Group Policy Management Console
- Windows Pro or Enterprise
- Web Browsers other than Edge (I used Google)
- AD Groups for All Employees and a user account.

---

**Purpose: Display a Specific Web Page** 

- Use a Service Account as login account
- The account should auto login when computer was rebooted.
- Web browser should startup automatically once logged in and in full screen.
- Set the computer to always be ON
- Restrict Logon for Service Account

---
# Activity 1: Set up Sysinternals - Autologon

Step 1: Open Active Directory

Step 2: Create a separate OU for service accounts. 

Step 3: Create service Accounts

Step 4: Create New User “Website Login”
<img width="786" height="557" alt="1 New OU - New User Created" src="https://github.com/user-attachments/assets/6e2e0082-7b33-4021-993a-36ee8c8f9c5e" />


Step 5: Under description put “Autologin to Websites”

<img width="531" height="74" alt="2 New User Created with description" src="https://github.com/user-attachments/assets/af983338-24d3-450e-8868-f52c5aec61d2" />


Step 6: Go to Windows client and download and install Sysinternals Suite tool

<img width="640" height="186" alt="4 Download systernals Suite" src="https://github.com/user-attachments/assets/97413bef-492b-4fd6-9039-1472ba11d350" />


Step 7: Extract it and set it up. Click on “Autologon”

<img width="463" height="507" alt="5 Download Autologon" src="https://github.com/user-attachments/assets/81436dae-3058-434b-bd0d-15edf650a2b2" />


Step 8: enter user name logon into “Auto logon - Sysinternals”

<img width="317" height="172" alt="6 login into Websitelogin user" src="https://github.com/user-attachments/assets/753951da-6159-429e-be5a-b6f0611e5677" />

Step 9: Successfully Configured

<img width="320" height="156" alt="7 successful login" src="https://github.com/user-attachments/assets/098d7b51-bee7-4915-bea4-d7d7769d5daf" />


Step 10: Verify it works. Restart  the computer. It should automatically login.

<img width="540" height="505" alt="9 should automatically login " src="https://github.com/user-attachments/assets/8ebed20a-67ef-496b-abcf-a5adc5f7cbe1" />
<img width="276" height="255" alt="8 Restart computer to test" src="https://github.com/user-attachments/assets/a380a204-540a-4586-b6af-28c799fe6daf" />

----

# Activity 2: Set up browser to startup with the webpage you need to display

Step 1:  Download google chrome.

<img width="368" height="122" alt="3 Download Google chrome browser" src="https://github.com/user-attachments/assets/68cd273d-a69b-47b9-9419-0618ea919672" />

Step 2: Open and go to settings

Step 3: On startup enter page you want to load. 

<img width="986" height="691" alt="10 Change startup page login " src="https://github.com/user-attachments/assets/ed79e944-be32-4f25-9679-28f426ee9e2d" />

Step 4: Verify by reopening google. it should automatically go that page.

Step 5: Click WIN + R

Step 6: Type in “Shell:startup”

<img width="410" height="215" alt="11 shell startup " src="https://github.com/user-attachments/assets/c2dadf3a-4e01-4003-8c12-a960fb0202c3" />

Step 7: This window is where you can put all the programs you want to open at startup.

<img width="795" height="613" alt="13 Should appear in folder " src="https://github.com/user-attachments/assets/e6ffd81f-d4ca-4ab1-b7a6-a824dac48165" />


Step 8: Next Type in Windows Search Bar, “Power and sleep Settings”.

<img width="799" height="627" alt="14 Change sleep settings" src="https://github.com/user-attachments/assets/921c454e-df18-4117-a914-569f5024b6bb" />


Step 9: Put the Sleep time top 2 hours.

Step 10: Verify it works. Restart computer.

Step 11: It should successfully Login and open google browser automatically on startup.

<img width="1236" height="953" alt="15 successful screen loadup" src="https://github.com/user-attachments/assets/9281aada-48ba-4eb7-a658-7911ded0a0f5" />

---

# Activity 3: Service Account GPO -Do not want anybody to log on.

Step 1: Open Group policy management console

Step 2: Right click Group Policy Objects. Click New

Step 3: Name it “Restrict Logon to Service Account”

<img width="1026" height="542" alt="16 GPO - New GPO Policy" src="https://github.com/user-attachments/assets/390fdb37-fb09-4c59-aa4f-7f0ddf782543" />


Step 4: Computer Configuration → Windows Settings → Security settings → Local Policies → User Rights → Deny Logon Locally

<img width="312" height="433" alt="17 User rights Assignment" src="https://github.com/user-attachments/assets/35db8f1c-696d-48ab-915c-f57a46c22c77" />


Step 5: Make sure that you have a group for All users so it will be easier to add group. “#All-Employees” Should have all Department staff under members of “#All-Employees”.
        
<img width="398" height="455" alt="19 Create Members of " src="https://github.com/user-attachments/assets/2d79cd61-0c2e-4608-a1f9-5e7550a8d456" />

<img width="757" height="526" alt="18 Setup Active Directory OU and groups correctly " src="https://github.com/user-attachments/assets/ab1f8419-2222-4a93-a3cc-a6e08690d4b9" />


Step 6: Click on Deny Logon Locally → Define the Policy Settings → Add user or Group → Select “#all-employees” → Apply and OK

<img width="413" height="507" alt="21 Select all #employees on Deny logon on GPOM" src="https://github.com/user-attachments/assets/62d5ee25-8fdb-4aa8-9950-7c9fd808187a" />


Step 7: Move Restrict Logon to Service Account to Under USA → Computers

<img width="268" height="99" alt="22 move Gpo to respected OU" src="https://github.com/user-attachments/assets/7d5e3886-370d-4adb-b171-731b91e44c16" />


Step 8: open command prompt and run gpupdate /force

<img width="698" height="135" alt="23 force update" src="https://github.com/user-attachments/assets/868c63de-e869-481e-88d0-049be55f8925" />


Step 9: Verify now. Log into a different user under Other User.


Step 10: It should say “ Not allowed”. Successful Test!

<img width="393" height="278" alt="24 Successful project Completion " src="https://github.com/user-attachments/assets/e1a12531-9cc0-4ee0-bad1-e5ef87706cf0" />
