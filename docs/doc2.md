---
id: doc2
title: Qruize Magic - Deployment Procedures
sidebar_label: How to Deploy QM (On-Premise)
---

## Prerequiste ##


##### a. Windows Server Version 2012 #####
##### b. Xampp version x64-7.3.19 (which includes apache webserver, mysql database and php) #####
##### c. Php version 7.3.19 #####


### Installation Process of the XAMPP Server ###
 
Step 1: To download the XAMPP server, visit the "Apache Friends" website in your web browser.
 
Step 2: Click on "XAMPP for Windows". Then, navigate the downloading location and the file will be automatically downloaded.
 
![XAMPP Installer](/img/QMDeployment/1.jpg)
 
Step 3: Double-click the downloaded file to launch the XAMPP installer.
 
![Launch XAMPP Installer](/img/QMDeployment/2.jpg)
 
Step 4: "Setup" window will appear on the screen. Then, click on the "Next" button.
 
![Setup XAMPP Installer](/img/QMDeployment/3.jpg)
 
Step 5: Select the components that you want to install and click on the "Next" button.
 
![Select components](/img/QMDeployment/4.jpg)
 
##### Note: By default, all components are selected in your XAMPP installation. 
 
Step 6: Choose a folder to install the XAMPP and click on the "Next" button.
 
![Installation folder](/img/QMDeployment/5.jpg)
 
Step 7: Uncheck the "Learn more about Bitnami for XAMPP" option and click on the "Next" button.
 
![Bitnaumi setup](/img/QMDeployment/6.jpg)
 
Step 8: "Ready to Install" window will appear on the screen, then click on the "Next" button.
 
![Ready to Install](/img/QMDeployment/7.jpg)
 
Step 9: Click on the "Finish" button.
 
![Finish](/img/QMDeployment/8.jpg)
 
Step 10: Select a language. (either English or German) and click on the "Save" button.
 
![Language](/img/QMDeployment/9.jpg)
 
#### Configuration Process of XAMPP Server ####
 
Step 1: Start the XAMPP control panel through the <b>"Run as administrator"</b> option.
 
Step 2: "XAMPP Control Panel" will appear on the screen and click on "Start" action to start the <b>"Apache"</b> and <b>"MySQL"</b> modules.
 
![Language](/img/QMDeployment/10.jpg)
 
##### Note:- #####
 
The default XAMPP server settings should work for most users. When you start the related modules (services) then, the color of the related modules (service) becomes change into the green color and the PID(s) and the Port(s) number will also be shown to the user.
 
![Language](/img/QMDeployment/11.jpg)

<b> Phalcon Installation: </b>
We need to install WAMP/MAMP/LAMP/XAMP according to your operating system. Below the installation is based on WAMP (Windows Apache MySQL PHP).
We install the following prerequisite:
1. Phalcon
2. Developer tools

<b>Installing Phalcon:</b>

Step 1: Download Phalcon from https://phalconphp.com/en/download for windows.
Download Phalcon dll file for Windows.

![Language](/img/QMDeployment/12.jpg)

Step 2: Unzip the folder in C:\Xampp\bin\php\php5.5.12\ext i.e. in extension folder of php.

![Language](/img/QMDeployment/13.jpg)

Step 3: Edit the php.ini file which is located at C:\wamp\bin\php\php5.5.12\php.ini with notepad or other similar editor.

![Language](/img/QMDeployment/14.jpg)

Step 4: Restart Apache server and we can see the Phalcon extension added.


<b>Installing Developer tools</b>

Step 1: Download developer tools from https://github.com/phalcon/phalcon-devtools of correct version. Extract in C:\ drive which looks like C:\phalcon-devtools-master.
Version info in XAMPP
Check by running XAMPP server then click on php info().

![Language](/img/QMDeployment/15.jpg)

![Language](/img/QMDeployment/16.jpg)

Step 2: Set environment variables for PHP and Phalcon developer tools.

![Language](/img/QMDeployment/17.jpg)

![Language](/img/QMDeployment/18.jpg)

![Language](/img/QMDeployment/19.jpg)

Step 3: Open cmd and type command "phalcon".

![Language](/img/QMDeployment/20.jpg)

Step 4: Create project demo using command.
1. phalcon create-project <project-name>.  

![Language](/img/QMDeployment/21.jpg)

![Language](/img/QMDeployment/22.jpg)

<b>Edit:</b> We edit the server config file,
1. Open apache's configuration file in text editor. The configuration files location at {wamp_dir}/apache/conf/httpd.conf.
2. Search for the following string: #LoadModule rewrite_module modules/mod_rewrite.so and uncomment it (remove the '#' sign).
3. Now search for another string AllowOverride None and replace it by AllowOverride All.
4. Finally save the changes and restart your wamp server.
Run- To check the successful installation of project we run project file located under directory file:///C:/wamp/www/demo/index.html and run on localhost.

![Language](/img/QMDeployment/23.jpg)

### QruizeMagic Configuration in Apache webserver ###

Step 1:
Get the latest build from qm team

Step 2: Create qm frontend and qm api content path as below in apache htdocs,

##### D:\qm\htdocs\qruize_magic_api 
##### D:\qm\htdocs\qruize_magic_ui 

Step 3: Create the apache virtual host in https-vhosts,
Open D:\qm\apache\conf\extra\httpd-vhosts and create virtual hosts as below,

<VirtualHost <ip address of your server>:81>
##ServerAdmin webmaster@dummy-host2.example.com
DocumentRoot "D:/qm/htdocs/qruize_magic_ui"
##ServerName dummy-host2.example.com
##ErrorLog "logs/dummy-host2.example.com-error.log"
##CustomLog "logs/dummy-host2.example.com-access.log" common
</VirtualHost>

<VirtualHost <ip address of your server>:82>
##ServerAdmin webmaster@dummy-host2.example.com
DocumentRoot "D:/qm/htdocs/qruize_magic_api_new/public"
##ServerName dummy-host2.example.com
##ErrorLog "logs/dummy-host2.example.com-error.log"
##CustomLog "logs/dummy-host2.example.com-access.log" common
</VirtualHost>

<b>Qruize Magic Database configuration</b>

open D:\qm\htdocs\qruize_magic_api_new\app\config\server.development file and create content as below,

database' => [
'adapter' => 'Mysql',
//'host' => 'localhost',
'host' => 'localhost',
'username' => '<db user name>',
'password' => '<password>',
'dbname' => 'qruize_magic_db',

<b>Qruizemagic Base URL Configuration</b>

open D:\qm\htdocs\qruize_magic_ui\js\config file and configure as below,

BASEURL = "enter qm api url here";

Example: BASEURL = "http://172.31.22.192:82";


<b>QM database import in mysql</b> 

Get the db dump from qm team and import into mysql dataabse 

<b>Checking qm working status</b>

Access the qm url <b>"http:// your server ip"</b>

Enter username and password

After sucessfull login you can ensure that qm is working fine


