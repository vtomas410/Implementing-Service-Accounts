# Implementing Service Accounts | Single Purpose Computers

Objectives:

- Gain practical experience with AD Service Accounts.
- Practice setting up and managing a single computer with a service account and special configurations.
- Use Sysinternals tools to setup and manage computers.

---

What is a Service Account?

A user account is created for a person to log into a computer, access files, and use applications. A service account is created for an application, Windows service, or automated task to perform specific functions. Service accounts allow programs to run automatically without requiring a person to log in. For example, a service account can run nightly backups or allow an application to access a database. Unlike regular user accounts, service accounts are designed for non-human use. They should have only the permissions necessary to perform their assigned tasks to reduce security risks.

For this Homelab we will create a computer that will display a program 24/7. It will be logged in with a service account and does not require a human to type anything in. It is used for display usually. 

Example: Kiosk, Screens at resturants

---

Prerequisites:

- Windows Server (VM)
- Active Directory Domain Services
- Group Policy Management Console
- Windows Pro or Enterprise
- Web Browsers other than Edge (I used Google)
- AD Groups for All Employees and a user account.

---

Purpose: Display a Specific Web Page 

- Use a Service Account as login account
- The account should auto login when computer was rebooted.
- Web browser should startup automatically once logged in and in full screen.
- Set the computer to always be ON
- Restrict Logon for Service Account

---
Activity 1: Set up Sysinternals - Autologon

Step 1: Open Active Directory

Step 2: Create a separate OU for service accounts. 

Step 3: Create service Accounts

Step 4: Create New User “Website Login”

Step 5: Under description put “Autologin to Websites”

Step 6: Go to Windows client and download and install Sysinternals Suite tool

Step 7: Extract it and set it up. Click on “Autologon”

Step 8: enter user name logon into “Auto logon - Sysinternals”

Step 9: Successfully Configured

Step 10: Verify it works. Restart  the computer. It should automatically login.

Activity 2: Set up browser to startup with the webpage you need to display

Step 1:  Download google chrome.

Step 2: Open and go to settings

Step 3: On startup enter page you want to load. 

Step 4: Verify by reopening google. it should automatically go that page.

Step 5: Click WIN + R

Step 6: Type in “Shell:startup”

Step 7: This window is where you can put all the programs you want to open at startup.

Step 8: Next Type in Windows Search Bar, “Power and sleep Settings”.

Step 9: Put the Sleep time top 2 hours.

Step 10: Verify it works. Restart computer.

Step 11: It should successfully Login and open google browser automatically on startup.

---

Activity 3: Service Account GPO -Do not want anybody to log on.

Step 1: Open Group policy management console

Step 2: Right click Group Policy Objects. Click New

Step 3: Name it “Restrict Logon to Service Account”

Step 4: Computer Configuration → Windows Settings → Security settings → Local Policies → User RIghts → Deny Logon Locally

Step 5: Make sure that you have a group for All users so it will be easier to add group. “#All-Employees”

Should have all Department staff under members of “#All-Employees”.

Step 6: Click on Deny Logon Locally → Define the Policy Settings → Add user or Group → Select “#all-employees” → Apply and OK

Step 7: Move Restrict Logon to Service Account to Under USA → Computers

Step 8: open command prompt and run gpupdate /force

Step 9: Verify now. Log into a different user under Other User.

Step 10: It should say “ Not allowed”. Successful Test!
