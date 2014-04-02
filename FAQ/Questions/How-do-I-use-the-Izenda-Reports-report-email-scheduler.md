#How do I use the Izenda Reports report email scheduler?

[[_TOC_]]

##Izenda Reports Scheduler Setup Instructions

It is recommended that you perform these installation steps on the Web Server on which Izenda Reports is installed.

First, we must allow the schedule controls to be shown in the Report Designer page.

* Navigate to the Izenda Reports settings.aspx page (e.g. http://yourhost/yourapp/settings.aspx)
* Click the "Email & Scheduling" tab
* Check the box next to "Show Schedule Controls"
* Click "Save to Izenda.Config" in the upper left-hand corner
* The schedule controls will now be shown in the report designer under the "Misc" tab
* If you set the Izenda Reports settings via code, then you will need to set the following settings, otherwise ignore the below C# line of code.

```csharp
Izenda.AdHoc.AdHocSettings.ShowScheduleControls = true;
```

The scheduler requires the use of the Izenda Scheduler executable that is found in the root of the directory you installed Izenda Reports in. You then need to add a scheduled task to your system that runs every minute. The task uses the Izenda Scheduler to access a page in our application that determines if any reports need to go out. The Izenda Scheduler executable does not actually send out the files or access anything else except for the specific page in our application that you give the .exe file as a parameter.

You must follow the steps below or the reports will not be e-mailed.

Click the "Start" button in Windows Server, then click on the"Control Panel" menu option, the "Control Panel" will then expand and show a larger menu, Find the menu option "Scheduled Tasks" and click on it, after it expands click "Add Scheduled Task", the "Scheduled Task Wizard" will start. The screen shots and captions below demonstrate how to enable the Izenda scheduler.

* Click on the Windows "Start Menu" and open the "Control Panel" 
* Click on the "Scheduled Tasks" menu option 
* Click "Add Scheduled Task" 
* The "Add Scheduled Task" wizard will start. Click "Next" 
* Select the Izenda scheduler program by clicking "Browse" 
* Browse to the folder to which you installed Izenda Reports and select the Izenda scheduler program ( IzendaScheduler.exe ) 
* Enter a name for the scheduled task and select the frequency 
* Set the start time and start date 
* Enter the user name and password of a user with administrative rights and Click "Next" 
* Check "Open Advanced Properties for this Task..." 
* Click "Finish" 
* Now we need to add the proper command line parameter into the "Run" box as indicated by the arrow. 
* IzendaScheduler.exe takes the path to the rs.aspx page as a parameter (ex: http://yourhost/yourapp/rs.aspx ) 
* Click "Apply" and then Click "Ok"

Now that you have setup the scheduler, we will need to setup Izenda Reports. There are two ways to do this. We strongly recommend using the settings page if possible. The settings can also be set in code with the Global.asax page.

##Setup using the Settings.aspx page

To use the Settings.aspx page in the application (recommended):

* Navigate to the Settings.aspx page in Izenda Reports (for example http://yourhost/yourapp/settings.aspx).
* Click the "Email and Scheduling" Tab
* Set the "Email From Address" field (e.g. admin@yourdomain.com).
* Check the "Show Schedule Controls" check box
* Enter in your SMTP relay server in the "Smtp Server" field (e.g. smtp.yourcompany.com).
* Open a report you want to schedule in the report designer, click the “Misc” tab of the report. The scheduler controls will be towards the bottom of the page. Enter the email addresses separated by commas. Set the report type and the repeat frequency. You must set the repeat frequency in order to schedule the report.
* Save the report again.
* The e-mail scheduler setup is now finished.

##Testing the scheduler

To test this, go back to a report you wish to schedule and click on it. Click the Misc tab of the report. The scheduler controls will be towards the bottom of the page. Enter the e-mail addresses separated by commas, then set the report type and the schedule frequency. Save the report again. Now go back to the Report List. Next to the report, you should see the schedule time for the report. Now we can also look at the scheduled tasks on the server.

* Using the DOS command line, navigate into the Izenda Reports root directory (for example, C:\web\IzendaReports) and run IzendaScheduler.exe "http://yourhost/yourapp/rs.aspx". This should return a list of scheduled reports in the DOS window.
* Navigate to the rs.aspx page in the application (for example, http://yourhost/yourapp/rs.aspx). Now add this to the end of the URL, ?run_scheduled_reports=30 (30 equals the frequency in minutes it will run). The url in the browser should read: http://yourhost/yourapp/rs.aspx?run_scheduled_reports=30
* This will return a list of scheduled reports into the browser window. In either case, you should receive the link to your scheduled report in your e-mail.

##Alternative Setup using code in ConfigureSettings()

To set the settings in code:

* Setup your SMTP Server in the Global.asax file inside of the ConfigureSettings() method by modifying some settings in it. The Global.asax file is found in the root of the directory to which you installed Izenda Reports.

```csharp
Izenda.AdHoc.AdHocSettings.SmtpServer = "INSERT IP ADDRESS HERE";
```

* Setup your e-mail report format string. This is the string that the user sees when the e-mail is sent to him. The {0} will be replaced with the report that the user has been scheduled to receive. Remember to replace "Host" with your domain, such as "SomeCompany.com" and "App" with your application name, such as "Reporting".

```csharp
Izenda.AdHoc.AdHocSettings.ScheduledReportsUrlFormatString="http://Host/App/reportviewer.aspx?{0}";
```
* Set the e-mail address all users will see when a report is scheduled and sent via e-mail.

```csharp
Izenda.AdHoc.AdHocSettings.EmailFromAddress="reports@somecompany.com";
```

* Lastly, setup the report scheduling controls to show in the “Misc” tab.

```csharp
Izenda.AdHoc.AdHocSettings.ShowScheduleControls=true;
```

To test this, go back to a report you wish to schedule and click on it. Click the Misc tab of the report. The scheduler controls will be towards the bottom of the page. Enter the e-mail addresses separated by commas, then set the report type and the schedule frequency. Save the report again. Now go back to the Report List. Next to the report, you should see the schedule time for the report.

##Security On Scheduled Reports

Scheduled reports only supports per-user security using the Link format.  Scheduled attachments will not apply hidden filters normally, but you can apply security through PreExecuteReportSet() based on the security of the report owner.  If per-user security is required, the Link format will require the user to login before seeing the report.