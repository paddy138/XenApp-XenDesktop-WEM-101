# **Training Overview** #
**Objective**

In this lab, you will discover how to build a snappy user experience, increase user density on any XenApp, XenDesktop environment, and learn how to manage a fast logon time (<15 s)
You will:

-	Understand WEM architecture
-	Learn how to configure CPU/RAM/IOPS optimizations
-	Learn how to replace user GPPs and login scripts

## Lab Environment ##
You should use this lab environment in the Demo Center:
*Application Virtualization with XenApp (MR 2.3)*


## Configure WEM optimizations and run test scenarios ##
Connect as a demo admin, either through the StoreFront site to launch XenCenter or connect from XenCenter directly if you have it installed.

Start server DNA1.

Connect to one of the XAWx servers (XAW1 or XAW2)

**NOTE:** The following steps are only designed for a POC or dev environment, not in production.

Download the "WEM-Examples.zip" file from GitHub and copy all files in the archive into a local temp folder, for example the “Documents” folder

**CPU idle step:**
Launch services.msc and stop Norskale Agent Host service in order to stop WEM optimizations. 
 
Launch WEM POC results.xlsx from your Documents folder

To avoid any Windows optimization side effects, launch and close each of the example files twice: 

- My Excel File.xlsx
- Test page with Chrome
- Test Page with Internet Explorer
- Workspace Environment Management_Technical_1.0.pptx
- XenDesktop Reviewer's Guide_Blade.docx

Use your smartphone to measure the “launch time” for each example file: time between the enter key stroke to the launch of the file, and time when the application is ready to use.

Open WEM POC result.xlsx previously copied in the documents folder
Go to the CPU tab.
Fill rounded numbers in the results excel file, on the first column:
 
- 100% CPU used, without optimizations step:
- Keep WEM service stopped,
- Right-click on the taskbar and launch Task Manager

From Windows Explorer, connect to \\WEMB\CitrixWEM-install\  and copy cpueater.exe to your desktop
Launch cpueater.exe
 
Click the On button, and check on Task Manager that the CPU is “eaten”

Use your smartphone to measure “launch time” for each example file: time between enter key stroke to launch the file and the time when the application is ready to use.

Click Off on CPUeater
Fill rounded numbers in the results excel file, on the second column:
 
100% CPU used, with optimization step:

Start services.msc and start Norskale Agent Host Service
 
Launch cpueater.exe
 
Click the On button, and check on Task Manager that the CPU is “eaten”

Use your smartphone to measure “launch time” for each example file: time between enter key stroke to the launch of the file and time when the application is ready to use.

Click Off on CPUeater
Fill in the rounded numbers in the results excel file, on the third column:
 
In the first part of the exercise, you have verified WEM CPU optimization benefits. Even though CPU was maxed out, we maintained the best possible performance level for end user activity.
This feature will be key to add more users on XenApp servers and maintain very good application responsiveness.
This step by step scenario can be easily done in a POC with customers.

**RAM optimizations:**

Close every sample application, and launch “My Excel File.xlsx”
Check immediately memory size on Task Manager, Details tab, Memory column:
 
Go to the RAM tab of “WEM POC results.xlsx” and fill this rounded number in MB, in this first column:
 
Redo same steps in point16 for every sample application:

- “Test page with Chrome” (add every Chrome process)
- “Test Page with Internet Explorer” (add every IE process)
- “Workspace Environment Management_Technical_1.0.pptx”
- “XenDesktop Reviewer's Guide_Blade.docx”

Report numbers in the RAM tab of “WEM POC results.xlsx”,
Wait for up to 5 minutes, without using these applications: WEM agent detects application activity, and do not apply any RAM optimization to “in use” application.
After at least five minutes, check the memory size of the applications running in task manager, and report the new numbers in the RAM tab of “WEM POC results.xlsx”
 
Memory footprint of running applications, but idle, has been deeply reduced.

These optimizations will apply to any running process and give an overall RAM usage reduction from 20% up to 50% on any Windows process

Bring Internet Explorer back into focus. 
Check there is no latency in accessing the optimized application and has good responsiveness. 
Check the memory size again in task manager and report new numbers in the RAM tab of “WEM POC results.xlsx”
 
## Configure WEM for a fast and resilient logon time ##

Download the " 	WEM-Config.zip" from GitHub and copy all files in the archive into a "C:\CitrixWEM-install\".

Connect to DNA1 server as the demo amdin accounts.

Launch the WEM Administrative Console

Connect to the server "dna1.citrix.lab" and then select the XenApp site to the right.
 
Click on Import Settings
 
Click Next
 
Click on Browse
Select “Default Recommended Settings” from 
“C:\CitrixWEM-install\Configuration Templates” folder
 
Click OK button
Check Agent Configuration Settings box,
 
Click Next button
Click on Import Settings button
 
And Click on Yes button on confirmation Window
 
Click on Finish button
On WEM management console, click on Advanced Settings => Configuration => Main configuration tab:
 
You have access to the WEM agent configuration. In this template, Agent will be launch at any user login, not for admin
Check automatic refresh setting in Advanced Options tab, and change it to 15 min
 
Click Apply button
Go to Configured users
 
Click Add button
Enter “user” and click Check Names

Select User1, User2, User3
 
Click OK
 
Click OK
Use Add button again, and add “domain users”.
You will obtain this final result: 
 
Go to Actions tab, select Applications
 
Use Import Actions button
 
Click Next button
 
Click Browse button
 
Select Sample applications
Click OK button
 
Select Applications check box and click Next button
 
Use Select All button and click Next
 
Click Import Actions button
 
Click Finish
New applications appear in Console
 
Add a printer queue:
Select Printers in the Actions list
 
Select Import Network Print Server button
Enter “SQL” as print server name
 
Click on Connect button
 
Click on Prefix check box, and add “SQL  - “
Click on Import Selected button
You should see this information in WEM console 
Select Network drives in Actions list
 
Use Add button
 
You will create a public share
Enter information as shown

- Name: Public
- Description: Public share
- Target Path: \\SQL\public
- Network Drive State: Enabled

Select Options tab and fill information as shown

- Display Name: Public Share
- Self Healing: Enable Automatic Self-Healing
 
Click OK button

Click Add button and fill information as shown for a new file share

- Name: Personal Folder
- Target Path: \\SQL\Personal\%username%

Go to Options tab, and fill information as shown

- Display Name: Public Share
- Self Healing: Enable Automatic Self-Healing
 
Click OK button
Select Filters tab, then Conditions. 
Click Add button, and fill information as shown

- Name: True if remote connection - Desktop student
- Filter Condition Type: Client IP Address Match
 
In Matching result field, you can add a range: 192.168.10.10;192.168.100.23-192.168.100.201
“;” is interpreted as an “or”
There are more than 75 different condition types, covering any customer technical needs
Click OK button
Select Rules
 
And click Add button
Fill information as shown

- Name: Student Desktop
- Filter Conditions: True if remote connection = Desktop student

Double click on Condition name or select it, and click on  
Click on OK button
Select Assignments tab
 
Double click on Domain users
 
On “Available” list, you see all Actions set.
Choose public drive and click  
Choose letter P
 
Click on OK button
Choose Personal folder, click on   and choose letter M
 
Click on OK button
Choose HP printer, click on  , and select Student Desktop rule, in the drop-down list
 
Click on OK button
Double click on User1, select Calculator icon and click on  
Accept “Always True” filter
 
Right click on “Create Desktop” and select Enable
 
Right click on “Pin to Taskbar” and select Enable
 
Double click on User2 and assign Notepad icon on Desktop and Start Menu
 
Open an Internet Explorer from your Student Desktop and connect to: http://sf1
Log in as a user1
Click on Desktops tab and launch the Shared Desktop icon: this will connect to XA1
Check:
WEM agent splashscreen, right after login
WEM agent Icon in Systray  
Calculator Icon on desktop,
Use “vuemrsav.exe” to check WEM agent instructions
Connect to XA1 with user1 again and check logon speed
Log off

Connect to WEMB and select Administration tab => users
 Click on Refresh button
Select Monitoring tab and click on Refresh button
 
This window gives a report of daily logon times for every user on any Windows environment
