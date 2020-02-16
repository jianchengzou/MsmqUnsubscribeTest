# MsmqUnsubscribeTest
Message Queue Fundamentals in .NET
Module 4 Setup Instructions
In Module 4 we extend our demo solution adding request-response and publish-subscribe messaging to our solution with MSMQ.
Pre-requisites 
The demo solution is delivered in Visual Studio 2013. 
The solution uses NuGet package restore to load packages during the build. 
To enable this in Visual Studio, open Tools…Library Package Manager…Package Manager Settings and ensure both options (Allow NuGet to download missing packages and Automatically check for missing packages during build in Visual Studio) are ticked.
The web project is set up to use IIS (not IIS Express), so you will need IIS installed, or you can change the configuration for the web project.
Messaging is done over MSMQ. You will need to have installed MSMQ (as a Windows component), and then create the following non-transactional queues: 
•	sixeyed.messagequeue.unsubscribe;
•	sixeyed.messagequeue.doesuserexist;
•	sixeyed.messagequeue.unsubscribe-crm – with multicast address 234.1.1.2:8001;
•	sixeyed.messagequeue.unsubscribe-fulfilment – with multicast address 234.1.1.2:8001;
•	sixeyed.messagequeue.unsubscribe-legacy – with multicast address 234.1.1.2:8001.
The Module 3 Setup Instructions detail how to install and configure MSMQ.
The validation in Module 4 is done using SQL Server (Express edition is fine); the connection string settings expect a local, unnamed instance. 
You will need to create a new database called Sixeyed.MessageQueue and deploy the entity model from Sixeyed.MessageQueue.Integration to the database, and then INSERT rows into the [Users] table with the valid email addresses you want to use.
 
Running the Solution
Build the solution and navigate to http://localhost/Sixeyed.MessageQueue.Web/unsubscribe in a browser window to submit the form and start the unsubscribe workflow. 
In the before solution, the browser will process the call without any validation, and with a single synchronous process for the unsubscribe workflow. 
In the after solution the website will validate the email address against the [Users] table. Run the StartHandlers.cmd batch file to start all the message handlers.
If you enter an unknown email address in the website you will get an “Unknown” page. Enter an email address which exists in the [Users] table and you will get a “Confirmation” page and you will see output in all the message handler condoles.

