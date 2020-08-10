---
id: doc3
title: Qruize Magic - Installation Procedures
sidebar_label: How to Use and Install QM
---

## <u>Contents</u> ##

1. Purpose
2. Required Software	
3. Installation – For Windows OS	
4. Installation – For Ubuntu OS	


1. Purpose

	The intended purpose of this Installation / Deployment Guide is to describe you the necessary steps for configuring the Qruize Magic application at your environment and make it operational.

2. Required Software

	Java 14

### <u>Installation of JAVA 14</u> ###

1. To check Java has already installed in your system, in the command prompt window, type **java –version** and press the enter key.
2. To newly install JAVA 14 in your windows system (64-bit), open the URL
	"https://www.oracle.com/java/technologies/javase/jdk14-archive-downloads.html" 
3. Click on the link shown below to download the Java package. Run the exe file and continue the installation process.

![java download page](/img/QMInstallation/1.jpg "1")

### <u>Installation – For Windows OS</u> ###

According to Qruize Magic, the installation implies adding the QM files in required location and it not implies of running any .EXE files. 
Installation of Local BOT:
1. You will receive a mail from Qruize that contains the link for downloading the files required for Qruize Magic installation. (OR)  You need to download and save QruizeMagic.zip (BOT setup) and Process files into your work environment. You are required to save it in a stable location (C or D drive). Below is the link to download the Qruize Magic folder setup.
 https://qruizemail.sharepoint.com/sites/qruizemagic/Shared%20Documents/QruizeMagic%20Setup%20file%20and%20document/QruizeMagic.zip

2. Unzip the **QruizeMagic.zip** file.
3. Open the bootstrap (properties file) from the path \QruizeMagic\config
4. Kindly make the following URL working in your environment. 
The spring.cloud.config.uri should be updated as  http://13.233.248.152:8182 .and key.entry should be 
set static instead of dynamic.

![spring.cloud](/img/QMInstallation/2.jpg "1")

5. As a next step, you need to set QM application path and Java JDK paths on your system environment variable. To do this:

     a) In the windows search field, type “Edit the System Environmental variables” and click on the enter button

     b) Click on the Environmental Variables… button in the Advanced tab

     c) In the user variables section, click on the New button

     d) To set QM application path on User variable, provide QM_HOME as variable name

     e) Set extracted base path up to QruizeMagic as Variable value.

     For example: C:\QruizeMagic

     f) Click on the OK button.

 **Setting environmental variable path for QruizeMagic**


 ![Environment variable](/img/QMInstallation/3.jpg "1")


**Setting environmental variable path for java JDK**

   g) To set Java JDK path on User variable, provide JAVA_HOME as variable name

   h) Set extracted base path up to jdk-14.0.1 as Variable value. 
   For example: C:\Program Files\Java\jdk-14.0.1

![Java Home](/img/QMInstallation/4.jpg "1")

 **Setting environmental variable path for java JDK bin folder**

i) To set Java path on system variable, double click on Path and set extracted base path up to bin folder as Variable value. Then click on the OK button.
For example: C:\Program Files\Java\jdk-14.0.1\bin

![JDK Bin file](/img/QMInstallation/6.jpg "1")


6. Locate to the extracted path manually up to **QruizeMagic** folder. 

![QruizeMagic](/img/QMInstallation/7.jpg "1")

7. Type cmd in the address bar and click on the enter button

![CMD QruizeMagic](/img/QMInstallation/8.jpg "1")

8. You can initiate batch file to initiate the bot (or) In the command prompt window, type the command:  **java -jar -Dspring.config.location=config\bootstrap.properties QruizeMagic-Robot-Service-v2.0.0.9.jar**

9. Note: PATH should be up to QruizeMagic folder. In this scenario, it is C:\QruizeMagic 

![CMD java command](/img/QMInstallation/9.jpg "1")

10. After entering the above command press the enter key in command prompt window to initiate installation process.

![CMD BOT Engine ](/img/QMInstallation/10.jpg "1")

Now the Qruize Magic robot service will be initiated and now you can open the below URL and execute the process. 
https://uatplatform.qruizemagic.com

### <u>Installation – For Ubuntu OS</u> ###

Installation of Local BOT:

1. You will receive a mail from Qruize that contain the links for downloading the files required for installing Qruize Magic in your system. 
2. You need to download and save QruizeMagic.zip (BOT setup) and Process files into your work environment. You are required to save it in a stable location.
3. Open the bootstrap.properties from the path /QruizeMagic/config
4. Kindly make the following URL working in your environment. 
The spring.cloud.config.uri should be updated as **http://13.233.248.152:8182** .and key.entry should be set static instead of dynamic.

![Spring Ubuntu OS](/img/QMInstallation/11UbuntuOS.jpg "1")

5. As a next step, you need to set QM application path on your system environment variable. To do this:

   a) Open terminal (command prompt window) 

   b) Type gedit ~/.bashrc and press enter key, this will open a bashrc file.

   c) At the end of the line, kindly add the below command to set the environment variable path.
	  export QM_HOME=/ home/selvam/Documents/QruizeMagic

![Export QMHOME](/img/QMInstallation/12.jpg "1")

   Here, “QM_HOME” is variable name **“home/selvam/Documents/QruizeMagic”** is location 
   of the QruizeMagic folder path. You need to give the path location where you saved the QruizeMagic folder.

   d) Save the changes and close the bashrc file.

   e) Close the terminal window.	

6. To run the QM dependency files, locate to the extracted path manually up to QruizeMagic folder and open it. Right click and select Open in Terminal option.
7. In the terminal page, type the below command: 
	**java -jar -Dspring.config.location=config/bootstrap.properties QruizeMagic-Robot-Service-v2.0.0.9.jar**

	**Note:** PATH should be up to QruizeMagic folder. In this scenario, it is /home/selvam/Downloads/
8. After entering the above command press the enter key in terminal window to initiate installation process.

![BOT Engine](/img/QMInstallation/13.jpg "1")

9. Now the Qruize Magic robot service will be initiated and now you can open the below URL and execute the process. 
**https://uatplatform.qruizemagic.com**