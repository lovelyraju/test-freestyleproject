


 


"Experience Seamless Streaming: Deploying Netflix's Sign-Up Page on Tomcat via Jenkins"
 
 

Deploying a Netflix Static Page in Tomcat Using Jenkins Freestyle Project as an Integration Tool
Requirements for Deploying an Application in Tomcat:
1.	Two Servers Setup: One server for Jenkins and another server for Tomcat.
2.	Jenkins Setup: Install and configure Jenkins on the Jenkins server.
3.	Tomcat Setup: Ensure Apache Tomcat is installed and configured on the Tomcat server.
4.	Build the Application: Use Jenkins to build the application, which will generate a WAR/EAR/JAR file.
5.	Deploy the Build Artifact: Transfer and deploy the WAR/EAR/JAR file to the Tomcat server for deployment.

Step-1: Launch Two Instances: Initialize two separate servers — one dedicated to Jenkins and the other for Tomcat.
Server Configuration:
Jenkins Server Setup: Install and configure Jenkins on the first server.
Tomcat Server Setup: Install and configure Tomcat on the second server.
Note: Ensure that the Tomcat server has similar configurations to the Jenkins server to maintain consistency in performance and security settings.
 

Step-2: Setting Up Jenkins 
🔗 Setting Up Jenkins - Click Here to Learn More
Step-3: To create a job in Jenkins and set up a repository, start by creating a new Freestyle project, then configure it by adding your repository URL and credentials under the Source Code Management section. Save your settings to finalize the job setup.
Note: Install git on Jenkins Server.

At the "Branches to build" option, the default branch name is set to "master." Make sure to modify it to the correct branch name accordingly.

 

Note: I have the Netflix-Signup repository in my GitHub. You can fork it to your own GitHub.
https://github.com/lovelyraju/test-freestyleproject.git


Step-4: Installing Java 1.8 (OpenJDK) and Maven on the Jenkins Server.
  


Step-5: Under Build Steps, configure the build process to compile your project, ensuring it generates the desired WAR, JAR, or EAR file upon completion.
 
 



Step-6: Build the job.
After building the code with "Invoke top-level Maven targets," you will get a packaged WAR file in the target folder. You should now deploy this WAR/JAR/EAR file in Tomcat.
 

Step-7: Setting Up Tomcat
Download java of any version
 
 

Download Tomcat file from dlcdn: wget (link address)
Example: wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.93/bin/apache-tomcat-9.0.93.tar.gz
You can download the file from path /tomcat/tomcat-9/v9.0.93/bin/
 

 

Untar the file
tar -zxvf apache-tomcat-9.0.93.tar.gz 
 
 

Go to the folder apache-tomcat-9.0.93 >> bin, and in the bin folder, you will find the startup.sh script to start Tomcat.
 

Access the public_Ip_addresss along with port number (8080).
 

To deploy the application, you must first log in. If you navigate to the manager, you'll receive an "Access Denied" message.
 

By default, the Manager is only accessible from a browser running on the same machine as Tomcat. If you wish to modify this restriction, you'll need to edit the Manager's context.xml file.

Before using the locate command to find the context.xml file, ensure the database is updated with the command: sudo updatedb. This will ensure all files, including context.xml, are indexed and searchable.
 

 

Open the context.xml file in the Vim editor and delete lines 21 and 22:
Open the File:
Launch the Vim editor with the command: vim context.xml
Navigate to the Lines:
Go to line 21 by typing: 21G in command mode.
Delete the Lines:
Delete line 21 by typing dd. This command deletes the current line.
Delete the next line (previously line 22) by typing dd again.
Save and Exit:
Save the changes by typing :wq and pressing Enter. This command writes the changes to the file and exits the editor.

 
 

After deleting the code 

Navigate to the conf folder, open the tomcat-users.xml file in the Vim editor, and add the necessary credentials.
 


Go to line 50, copy the next three lines, paste them into the tomcat-users.xml file, and modify the credentials as necessary.
 
Add the role names manager-gui and manager-script, set the username as tomcat, and add a password. Assign the roles manager-gui and manager-script under the roles section.
 
Note: Whenever you change the configuration, you should restart the server. Since you've modified the configuration, go to the bin directory and restart the server.
 

Now, when you log in to the Tomcat dashboard, you should enter the credentials you configured.
 
Below is Tomcat dashboard.
 










Step-8: Deploy the WAR/EAR/JAR File in Tomcat
Install the "Deploy to Container" Plugin:
Go to the Jenkins dashboard.
Navigate to Manage Jenkins > Manage Plugins > Available.
Search for the "Deploy to Container" plugin and install it.
Configure the Job:
After installing the plugin, return to your job on the Jenkins dashboard to configure the deployment settings.

 






Step-9: 
Here's a refined version of your instructions for configuring Jenkins to deploy using the "Deploy to Container" plugin:
1.	Navigate to Job Configuration:
o	Go to your job in Jenkins and click on Configure.
2.	Set Up Build Steps:
o	Scroll to Build Steps and proceed to Post-build Actions.
3.	Configure Deployment:
o	Select Deploy war/ear to container from the dropdown menu. This option is available only if you have previously installed the "Deploy to Container" plugin.
 




To configure the deployment of your packaged WAR/EAR file in Jenkins and specify the display name or application name in Tomcat.
 

Click on "Tomcat 9.x Remote" and add the Tomcat credentials.
 


Enter the credentials for Tomcat.
 

 



Step-10: Build the job now, and you'll see a file displayed under the name 'netflix'.
Before build the job, Tomcat dashboard:
 

After building the job
If you access the application Netflix, you’ll able to access the application.
 
Step-11: Access the application.
 

 
