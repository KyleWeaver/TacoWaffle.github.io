---
layout: docs
title: Developer Setup: e-PPE
section: dev
---

*The table of contents, scraped from rest of document
{:toc}


The intent of this document is to provide developers with instructions for setting up a development environment for the e-PPE.

# Before you Begin

You will need the following from the project lead:
* Access to the SDI server.
* Stash account for accessing the remote repository.
* Jira account for creating and resolving tickets/bugs.

## Required Software

* Tomcat 7
* Java jdk-7u45 (in S:\Projects\PrivIT\Development Resources\Java)
* Maven 3
* ImageMagick  (in S:\Projects\PrivIT\Development Resources)
* MySQL 5.5 (or higher)
* SourceTree
* IntelliJ IDEA
* MySQL Workbench (comes with MySQL installer)



# Start Here

You must have successfully installed the required software and have a Stash account to continue.


## Create a local repository for the e-PPE

1. Open SourceTree and click "Clone/New".

2. Source Path/URL: https://sdi.e-ppe.net/stash/scm/eppe/eppe.git
	
  

## Configuring Tomcat

1. Copy the following files from S:\Projects\PrivIT\Development Resources\Tomcat.
	* context.xml
	* server.xml
	* hazelcast.xml
		
2. Paste them into the conf folder of your local instance of Tomcat.
	
3. Open context.xml and set the value of the "rootDomain" parameter to "[yourFirstName].dev" and the "pathToImageMagick" parameter to the path to your local installation of ImageMagick. 
	ex.

	* \ <Parameter name="rootDomain" value="russ.dev" override="true"/>
	* \ <Parameter name="pathToImageMagick" value="C:\Program Files\ImageMagick-6.8.3-Q16" override="true"/> \
			
4. Copy the following jars from S:\Projects\PrivIT\Development Resources\Tomcat.
	* mail-1.4.5.jar
	* mysql-connector-java-5.1.29.jar	
	
5. Paste them into the lib folder of your local instance of Tomcat.
	
6. Copy the keys folder from S:\Projects\PrivIT\Development Resources\Tomcat.
	
7. Paste it into the root folder of your local instance of Tomcat.
	

## Java Security Jars	 
	
1. Copy both jars from S:\Projects\PrivIT\Development Resources\Java\UnlimitedJCEPolicy and paste them into jre\lib\security folder of your installation of jdk1.7.0_45.
	
	
## Create database

1. Open MySQL Workbench and create a new database named "eppe_local".
	
2. Create a new user 'eppe' using password 'eppe' and grant access to the new database. You can use the commands below:
	* create user 'eppe'@'localhost' identified by 'eppe';
	* grant all on eppe_local.* to 'eppe'@'localhost';
		
	
## Importing and configuring the project in IntelliJ	
*Import the Project*
	
1. Open IntelliJ and select File->Import Project.
		
2. Select the root folder of your local e-PPE repository and click OK. (Most likely: C:\Users\[yourName]\Documents\eppe)
		
3. Select "Import project from external model", choose Maven and click Next.
		
4. Click Next again.
	
5. Confirm "com.privit.eppe:eppe:x.xx.x" is selected and click Next.
		
7. Select 1.7 as the project SDK and click Next.
	- If none are listed, add a new JDK by clicking the plus button and selecting the path to your jdk-7u45 root.
		
8. Confirm the Project name and location and click Finish.
	
*Configure Project Structure*
	
9. Select File->Project Structure.
	
10.	Select Project and confirm the Project language level is set to 7.0 (as of 7/24/2014).
 
11. Select modules and mark the .idea folder as excluded.
		
12. Add the following Facets to the appropriate module by selecting Facets and clicking the plus sign.
	- Hibernate
	- Spring
	- Struts 2
 
13. Under Modules, add the corresponding configuration files to each facet.
 
*Configure Tomcat for deployment from IntelliJ*
 	
14. Select Run->Edit Configurations.
	
15. Add a new Tomcat server by clicking the plus sign in the top left corner and selecting Tomcat Server->Local.
		
16. Click Configure next to the Application server option and create a new Tomcat server pointed to the root directory of your local installation of Tomcat.
		
17. For VM options enter: -ea -server -Xms256m -Xmx512m -XX:MaxPermSize=128m -XX:NewRatio=3 -XX:MaxTenuringThreshold=15 -XX:+HeapDumpOnOutOfMemoryError -Ddame.crypto.keyPath="C:\Program Files (x86)\apache-tomcat-e-ppe\keys" -DappPath="C:\Program Files (x86)\apache-tomcat-e-ppe" -Djava.net.preferIPv4Stack=true -Dhazelcast.config="C:\Program Files (x86)\apache-tomcat-e-ppe\conf\hazelcast.xml"
		
18. Under "Before launch: Make, Build Artifacts" section, click the plus sign and add 'Build eppe:war exploded artifact'.
		
** You should now be able to run the application from IntelliJ by selecting Run or Debug **
	
## Using the e-PPE for the first time

1. Add the following lines to your hosts file. (C:\Windows\System32\drivers\etc\hosts)
	* 127.0.0.1 www.[yourFirstName].dev
	* 127.0.0.1 admin.[yourFirstName].dev
		
2. In your browser's address bar type: admin.[yourName].dev:8080
	
3. Sign in using the credentials:
	* email: root@priv-it.com
	* password: root
	
4. Select User Management->Manage System Administrators and create a new user using your email.
	
	
# More	

SDI Server:
* The Software Development Infrastructure (SDI) Server is a server hosted in the Infinity datacenter where we host tools and resources related to the development of the e-PPE.
* Add "10.10.31.50 sdi.e-ppe.net" to your hosts file. (C:\Windows\System32\drivers\etc\hosts)



	
	
	
	
