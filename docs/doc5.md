---
id: doc5
title: Qruize Magic - Creation of an Automation Process
sidebar_label: How to Build a Automation Process?
---

## <u>Prerequisites</u> ##

### <u>About the Document</u> ###

This document helps you to understand different actions available in Qruize Magic.
### <u>What is a JSON File?</u> ###

JSON is a file that stores simple data structures and objects in JavaScript Object Notation (JSON) format, which is a standard data interchange format. It is primarily used for performing automation in web, desktop and mobile applications. JSON files are lightweight, text-based, human-readable, and can be edited using a text editor.

### <u>JSON Structure </u> ###

The standard Json structure looks like:
	
	"StepName": 
	{
	    "Key1":"Value1",
	    "Key2": "Value2",
	     . . . .
	    "KeyN": "ValueN"
	}

### <u>Major Components of the Qruize Magic Folder</u> ###


Below are the important folders and files present in the Qruize Magic folder.

a. **.qm,** b. **config,** c. **lib,** d. **logs,** e. **bat,** f. **Executable Jar file (QruizeMagic-Robot-Service-v2.0.12.1),** g. **Zip.jar,** h. **process** and i. **temp**.

Let us see each and every items in detail.

**.qm**:
This folder consists of plugins that require for executing the process. Each plugin consists of classes and libraries for the respective functionality. To use any Plugin actions for creating a process, you are required to add respective plugin details with version in the profile.json file.


**Config**:
This folder consists of two major files,

**I.** Application.properties - It consists of property fields that is to be used as input for the bot agent.

Below is the sample of an Application configuration file

	-------------Application Configuration---------------------
	#Robot Server port config
	spring.application.name=robot 
	server.port = 9090 //tomcat is started on the mentioned port

	#configuration server details
	spring.cloud.config.uri=http://13.233.248.152:8182 //the uri of the platform configuration 
	service that you want to connect with.
	robot.customplugin.path=plugin 

	#Scheduler Config  //this is java auto scheduler which will run at the scheduled time.
	tenant.id = 210 
	process.name = processname
	schedule.time = 300000 //time in milli second, within this given time interval the scheduled
	process will run.
	process.scheduler = false //true, if you want auto scheduler feature.



	#auto //To fetch the key automatically. Here, the fetching of dynamic key will take place and 
	no manual key configuration at startup is required. 
	E.g. On conditions like ECS environment.
	key.entry=static //make it dynamic if you want this feature.

	key.authenticate.url=n/a //the url of the key service.

	key.fetch.url=n/a //the url of the key service to fetch the key.

	key.return.url=n/a //the url of the key service to return the key.

	key.username=n/a //the username allotted for auto key feature.

	key.password=n/a //the password allotted for auto key feature.

	auto.process.name= n/a //the process name.

	auto.tenant.id = n/a //the tenant id allotted.

	auto.result.update = false //true if you want to see result update in platform.

	auto.result.update.variable.name = n/a //the variable name to store result id.

	#Plugin List - Studio //the list of plugins for studio purpose only
	plugin.list = msoffice.actions:v1.0.0.3,pdf.actions:v1.0.0.1,ocr.actions:v1.0.0.6,
	mail.actions:v1.0.0.5



**II. Key** - This file contains the license key which configured to the process.

**lib**:
This folder contains driver files of different browsers. 

Eg: chromedriver for Chrome browser and geckodriver for Firefox. 
It also contains library files that required for your process creation. For Eg: If you want extract details from PDF, then you can add the tesseract library inside this folder.

**logs**:
This folder contains the log information of the executed processes along with the timestamp.

**.bat file**: 
Double click on the batch file will initiate the Bot agent in your system.
 
**zip.jar**: 
Once the process is created, you are required to zip the process folder. Only then you can upload it in QM portal.

C:\QruizeMagic>java -jar zip.jar C:\QruizeMagic\process\PDFextraction process

**temp**:
During bot agent runtime, the temporary files will be stored inside this folder.

**Process**: 
You required to upload Process.zip file in QruizeMagic platform. This Process file consists of Script folder, variable folder, profile.json file, and Main.json file.
Once the Process execution is initiated, as a first step, the profile.json file will be processed by the bot. Let us now see the components one by one.

a) **profile.json**: 
This json file expresses plugin dependencies required, any run time input parameters used, password encryption flag, and execution trigger types.

Following is the sample **profile.json** file structure with description.

| Fields in profile.json | Description |
|-|-|
| { | Initializing profile.json |
| "name": "QMProcess", | Name of the process |
| "description": "welome to qruizemagic process creation", | Process description |
| "main": "Main.json", | Initializing Main.json file |
| "processDefinitionVersion": "1.0.2", | The version of the process is defined here. If any changes done in the process then the version need to be changed |
| "dependencies": [ | Plugin dependency part start here. All the required plugins along with version should be mentioned inside this. |
| "OCR_actions:v1.0.0.2", | Plugin used for this process and version detail of the plugin. Every version has some additional features in it. Based on the client requirement the version will be provided |
| "web_ui_actions:v1.0.0.11" | Plugin used for this process and version detail of the plugin. |
| ], | Plugin dependency part is closing here. |
| "runtimeOptions": { | Initializing runtime options  |
| "runtimeInputParam": [{ "field": "Receivermail_ID", "type": "text", "isEncrypt": true } ], | You can use this argument when you want to provide the input only at the time of process upload. For eg: If you want to send the report to certain mail id(s) then you need to provide the receiver mail ID in the Receivermail_ID field |
| "elicitOptions": { | Initializing elicit options |
| "triggerType": "API", | Trigger type used for process execution. “API” is for initiating process execution using button click. “SCHEDULER” is used to schedule the process to run at user specific time without manual trigger |
| "IsAttachmentRequired": true, | To check whether the attachment is required for this process. “True” defines this process requires attachment and “False” defines no attachment required |
| "AttachmentTypes":["jpg"], | The file type of the attachment |
| "arguments": [{ "field": "portal_username", "type": "text", }, { "field": "portal_password", "type": "password", }] | If you want to run the process with changeable input for every execution, you can use this argument. This will enable the argument option in QM platform. For eg: This helps you to execute the same process with different login credentials |
| } } } | Closing of elicit option, runtime option and profile.json |





b) **Main.json**: 
Main.json and the files inside the script folder play a major role in process execution. It sets the entry point for your RPA automation. This file consists of high level steps that involve in process execution in a structured way.

Example: For sending mail from a gmail account to different mail ids, the following major steps should be used.

**i. OpenBrowser** – To open the browser

**ii. Login** – Enter valid username and password

**iii. Compose Mail** – Mail composing includes set details in To, CC and Subject, and mail content fields. Click on the Send button.**

**iv. Logout** – Logout from gmail account

**i. OpenBrowser**:
Here is the sample script used for opening the gmail browser in the Main.json where the script itself contain the complete functionality for opening browser.

Open the web browser

|  			 Fields 		                               |  			 Description 		                                                                                                                            |
|-----------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|
|  			 "OpenBrowser": 		                       |  			 Unique 			step name 		                                                                                                                       |
|  			 { 		                                    |  			  			 		                                                                                                                                      |
|  			 "referenceId":"M4CR-9FZW-5U8G-N2P3", 		 |  			 Unique 			ID of the plugin. Each plugin has different ID. Based on this ID 			the plugin will be redirected. 		                                 |
|  			 "category": 			"Web UI Actions",  			 		      |  			 Category 			of a plugin 		                                                                                                                   |
|  			 "subCategory":"Selenium", 			 			 		          |  			 Denotes 			that the selenium actions were used 		                                                                                            |
|  			 "actionType": 			"OpenBrowser",  			 		       |  			 declaring 			the action name as OpenBrowser 		                                                                                               |
|  			 "browserType": 			"chrome", 		             |  			 the 			browser type you want to open the URL 		                                                                                              |
|  			 "url": 			"https://gmail.com", 		          |  			 URL 			you want to open 		                                                                                                                   |
|  			 "scope": 			"ACTION" 		                    |  			 Here 			in this above script, the scope is declared as ACTION, 			so the section contains the complete functionality of opening the 			browser. 		 |
|  			 } 		                                   |  			  			 		                                                                                                                                      |


**Note**: Here in this above script, the scope is declared as ACTION, so the section contains the complete functionality of opening the browser. 

**ii. Login**:
Following is the script used in the Main.json for Gmail login where the script contains only the path of the of the script which actually used for login.
If the scope is declared as GROUP, then the file inside the script folder will get executed. 

Login to the gmail

|  			 Fields 		     |  			 Description 		     |
|-|-|
|  			 "Login": 			{ 		        |  			  			 		        |
|  			 "referenceId":"M4CR-9FZW-5U8G-N2P3", 			 			 		           |  			 Unique 			ID of the plugin. Each plugin has different ID. Based on this ID 			the plugin will be redirected. 		           |
|  			 "category": 			"Web UI Actions",  			 		           |  			 Category 			of a plugin 		        |
|  			 "subCategory":"Selenium", 			 			 		           |  			  			 		        |
|  			 "scriptPath": 			"/script/login.json",  			 		           |  			 Path 			of actual script file 		        |
|  			 "scope": 			"GROUP" 		        |  			 If 			the scope is declared as GROUP, 			then the file inside the script 			folder will get executed. Only the path of the file to be executed 			is declared in the Main.json file. 		                 |
|  			 } 		     |  			  			 		        |

Only the path of the file to be executed is declared in the Main.json file.


Following are the actual script file contains gmail login functionality.
      
**Wait till** the specific element appears

|  			 Fields 		     |  			 Description 		     |
|-|-|
|  			 "wait_elementVisible1": 			{ 		        |  			  			 		        |
|  			 "referenceId": 			"M4CR-9FZW-5U8G-N2P3", 		        |  			 Reference 			ID of the wait action 		        |
|  			 "category": 			"Web UI Actions", 		        |  			  			 		        |
|  			 "subCategory": 			"Selenium", 		        |  			  			 		        |
|  			 "actiontype": 			"wait", 		        |  			  			 		        |
|  			 "scope": 			"ACTION", 		        |  			  			 		        |
|  			 "executionType": 			"Driver", 			 			 		              |  			 Execution 			type allows the developer to assign the execution method for the 			intended automation event. ‘Driver’ - To make direct calls to 			the browser using the browser’s native support (Locators) and 			‘Script’ – To use ‘JavaScript Executor’ 		                 |
|  			 "selectType": 			"Condition", 		        |  			  			 		        |
|  			 "conditions": 			[{ 		        |  			  			 		        |
|  			 "attr": 			"XPATH", 		        |  			 Defining 			attribute in the JSON will enable the bot to find and match the 			elements in your web page that it needs to interact during the 			automation. The various attributes you can define includes ID, 			xpath, CSS, or script 		                 |
|  			 "value": 			"//*[@id="identifierId"]", 		        |  			 Value 			helps in defining / specifying the equivalent value from the 			webpage for the defined attribute (E.g. XPath, ID, CSS, 			Javascript, etc)   			 		                 |
|  			 "selectType": 			"visibilityWait", 		        |  			  			 		        |
|  			 "delayInMinutes": 			"5" 		        |  			  			 		        |
|  			 }] 			 }      |  			  			 		        |



Enter **user name** in the field

|  			 Fields 		     |  			 Description 		     |
|-|-|
|  			 "Username": 			{ 		        |  			  			 		        |
|  			 "attr": 			"XPATH", 		        |  			  			 		        |
|  			 "referenceId": 			"M4CR-9FZW-5U8G-N2P3", 		        |  			  			 		        |
|  			 "category": 			"Web UI Actions", 		        |  			  			 		        |
|  			 "subCategory": 			"Selenium", 		        |  			  			 		        |
|  			 "scope": 			"ACTION", 		        |  			  			 		        |
|  			 "applicantkey": 			"name@gmail.com", 		        |  			 Applicant 			key is a property used to get a value from application and save it 			as a variable. You can use this value in required place. Eg. 			Insert the value in excel. If any variable created while writing 			automation steps, you can declare those variable in Variables JAVA 			file and compile it into CLASS file. Four different ways for set a 			value.  			  			 1. 			“name@gmail.com” 			– Hard code input,  			  			 2. 			#datagrid(variableName) 			– 			It will retrieve the value from variable,  			  			 3. 			#runtimeinput(variableName) 			– 			It will get the value from runtimeInputParam (.profile.json) only 			at the time of process upload  			  			 4. 			#arguments(variableName) 			– 			arguments is used when the process have changeable inputs for 			every execution. This will enable the argument option in QM 			platform. 		                                                                                         |
|  			 "value": 			"//*[@id="identifierId"]", 		        |  			  			 		        |
|  			 "actiontype": 			"setText", 		        |  			 Action 			is used to set the value in the field 		        |
|  			 "executionType": 			"Driver" 		        |  			  			 		        |
|  			 }			 			 		           |  			  			 		        |



Click on the **Next button** after entering the user name

|  			 Fields 		     |  			 Description 		     |
|-|-|
|  			 "ClickNextUID": 			{ 		        |  			  			 		        |
|  			 "referenceId": 			"M4CR-9FZW-5U8G-N2P3", 		        |  			  			 		        |
|  			 "category": 			"Web UI Actions", 		        |  			  			 		        |
|  			 "subCategory": 			"Selenium", 		        |  			  			 		        |
|  			 "scope": 			"ACTION", 		        |  			  			 		        |
|  			 "attr": 			"XPATH", 		        |  			  			 		        |
|  			 "value": 			"//*[@id= ‘identifierNext’]", 		        |  			  			 		        |
|  			 "actiontype": 			"click", 		        |  			 Click 			action type is used to click the next button 		        |
|  			 "executionType": 			"Driver" 		        |  			  			 		        |
|  			 }			 			 		           |  			  			 		        |



 Entering the **password** in the password field

|  			 Fields 		     |  			 Description 		     |
|-|-|
|  			 "Password": 			{ 		        |  			  			 		        |
|  			 "attr": 			"XPATH", 		        |  			  			 		        |
|  			 "referenceId": 			"M4CR-9FZW-5U8G-N2P3", 		        |  			  			 		        |
|  			 "category": 			"Web UI Actions", 		        |  			  			 		        |
|  			 "subCategory": 			"Selenium", 		        |  			  			 		        |
|  			 "scope": 			"ACTION", 		        |  			  			 		        |
|  			 "applicantkey": 			"password", or #datagrid(variableName), or  			 #runtimeinput(variableName), 			or #arguments(variableName) 		              |  			 Four 			different ways for set a value. 1. “password” 			– Hard code input, 2. #datagrid(variableName) 			– 			It will retrieve the value from variable, and 3. 			#runtimeinput(variableName) 			– 			It will get the value from runtimeInputParam (.profile.json) only 			at the time of process upload and 4. #arguments(variableName) 			– 			arguments is used when the process have changeable inputs for 			every execution. This will enable the argument option in QM 			platform. 		                                         |
|  			 "value": 			"//*[@id="password"]/div[1]/div/div[1]/input", 		        |  			  			 		        |
|  			 "actiontype": 			"setText", 		        |  			  			 		        |
|  			 "executionType": 			"Driver" 		        |  			  			 		        |
|  			 }   |  			  			 		        |



Click on the **Next button** after entering the **password**

	"ClickNextUID": {
	"referenceId": "M4CR-9FZW-5U8G-N2P3",
	"category": "Web UI Actions",
	"subCategory": "Selenium",
	"scope": "ACTION",
	"attr": "XPATH",
	"value": "//*[@id= ‘passwordNext’]",
	"actiontype": "click",
	"executionType": "Driver"
	}

**iii. ComposeMail**: Click on the **compose mail** button

	"ClickComposeMailBTN": {
	"attr": "XPATH",
	"referenceId": "M4CR-9FZW-5U8G-N2P3",
	"category": "Web UI Actions",
	"subCategory": "Selenium",
	"scope": "ACTION",
	"value": "//*[@id="composeMail"]",
	"actiontype": "click",
	"executionType": "Driver"
	} 


Enter **mail id** in the **TO** field


	"Tomail": {
	"attr": "XPATH",
	"referenceId": "M4CR-9FZW-5U8G-N2P3",
	"category": "Web UI Actions",
	"subCategory": "Selenium",
	"scope": "ACTION",
	"documentGridKey": "toname@gmail.com",
	"value": "//*[@id="ToMail"]",
	"actiontype": "setText",
	"executionType": "Driver"
	}


Enter **mail subject** in the Subject field
Fields

	"Mailsubject": {
	"attr": "XPATH",
	"referenceId": "M4CR-9FZW-5U8G-N2P3",
	"category": "Web UI Actions",
	"subCategory": "Selenium",
	"scope": "ACTION",
	"referenceId": "M4CR-9FZW-5U8G-N2P3",
	"category": "Web UI Actions",
	"subCategory": "Selenium",
	"scope": "ACTION",
	"documentGridKey": "MailSubject", 
	"value": "//*[@id="Subject"]",
	"actiontype": "setText",
	"executionType": "Driver"
	}


Enter **mail Content** in the respective field
Fields
		
	"Mailcontent": {
	"attr": "XPATH",
	"referenceId": "M4CR-9FZW-5U8G-N2P3",
	"category": "Web UI Actions",
	"subCategory": "Selenium",
	"scope": "ACTION",
	"documentGridKey": "MailContent", 
	"value": "//*[@id="Subject"]",
	"actiontype": "setText",
	"executionType": "Driver"
	}


Click on the **Send** button
Fields

	"ClickSend": {
	"attr": "XPATH",
	"referenceId": "M4CR-9FZW-5U8G-N2P3",
	"category": "Web UI Actions",
	"subCategory": "Selenium",
	"scope": "ACTION",
	"value": "//*[@id="SendMail"]",
	"actiontype": "click",
	"executionType": "Driver"
	}

**iv. Logout**:
Click on the **Menu** button
Fields

	"ClickMenu": {
	"attr": "XPATH",
	"referenceId": "M4CR-9FZW-5U8G-N2P3",
	"category": "Web UI Actions",
	"subCategory": "Selenium",
	"scope": "ACTION",
	"value": "//*[@id="menubutton"]",
	"actiontype": "click",
	"executionType": "Driver"
	} 


Click on the **Logout** button from the Menu
Fields

	"ClickLogout": {
	"attr": "XPATH",
	"referenceId": "M4CR-9FZW-5U8G-N2P3",
	"category": "Web UI Actions",
	"subCategory": "Selenium",
	"scope": "ACTION",
	"value": "//*[@id="Logout"]",
	"actiontype": "click",
	"executionType": "Driver"
	} 














**c) script Folder**
This folder consists of the actual script file(s) in JSON where the path is given in main.json.
Instead of writing all the steps in mail.json, you can write all steps in .json files  and place it inside the script folder. Further you should specify the path along with process name in main.json.
Eg: "scriptPath": "/script/FillingtheOnlineForm.json", //path of actual script file

**d) variable Folder**
This folder consists com, io folders and PluginFunction and Variables JAVA files. If any variable created while writing automation steps, you can declare those variable in this Variables JAVA file and compile it into CLASS file. com and io folders consists of library files, and PluginFunction file are required for compiling the variables.JAVA file.

**e) Exception.json**
This file contains the json steps which will be executed when exception occur during process execution. While creating the process steps in json, exception script should be added as shown below.
		
		"onError": [
			"create_datatable1",
			"add_header_1",
			"add_row,Get_property",
			"Write_to_excel",
			"sendNotificationMail"
		], 

















**4. Action type**: Action type is a property to define the required mouse and keyboard events, to be executed on web, desktop, mobile applications. The various action type supported is listed in the below section.

**Supported Actions**

**Web UI Automation Plugin**

|  			 No 		     |  			 Action 			Name 		        |  			 Description 		     |
|-|-|-|
|  			 1 		     |  			 OpenBrowser 		     |  			 This 			will help you to open the browser 		        |
|  			 2 		     |  			 wait 		     |  			 It 			makes webdriver to wait for certain time before proceeding to the 			next action.  			 Following 			three conditions are available for the wait action.  			 Visibility 			wait 			is like explicit wait which will wait till some pre built 			condition become true. Eg. Wait for elements to become clickable, 			visible, invisible, etc. Maximum time out should be given in 			delayInMinutes parameter.  			 LoadingMinutes 			will wait for default time of 2 seconds.  			 isDocumentReady 			will 			wait till the last element get loads in the webpage. 		                                                  |
|  			 3 		     |  			 setText 		     |  			 It 			will set the value in the input field.  			 		           |
|  			 4 		     |  			 selectItem 		     |  			 It 			will select one or multiple options from a dropdown list. 		        |
|  			 5 		     |  			 getText 		     |  			 It 			will fetch data from the application and stores it as a variable. 			The variable name should be mentioned as applicant key. 		           |
|  			 6 		     |  			 click 			 			 		           |  			 It 			will click on the UI element with respect to the attribute given. 			It is same as the mouse left click on the required element. 		           |
|  			 7 		     |  			 Hoverclick 		     |  			 It 			will click on the mouse hover element. It will trigger the base 			element first and then click on the hover element. 		           |
|  			 8 		     |  			 doubleClick 		     |  			 It 			will double click on the UI element with respect to the attribute 			given. It is same as placing mouse pointer on the required element 			and clicking the mouse left button twice. 		              |
|  			 9 		     |  			 hover 		     |  			 It 			will move the mouse from its current position to the given offset 			(Horizontal and Vertical) position. It is similar to mouse hover 			on an element. 		              |
|  			 10 		     |  			 switchToWindow 		     |  			 It 			will switch our focus control from one window to another window. 			Usually, it is used to switch over from main window to newly 			opened window. 		              |
|  			 11 		     |  			 Enter 		     |  			 It 			will press the enter key through selenium webdriver. It is similar 			to pressing the enter button in the keyboard. 		           |
|  			 12 		     |  			 focusEnter 		     |  			 It 			will move on to the specific element and click on it. 		        |
|  			 13 		     |  			 NavigateElement 		     |  			 It 			will move the focus from one element to another. It is similar to 			pressing the TAB button in keyboard. 		           |
|  			 14 		     |  			 selectradio 		     |  			 Handles 			togging of radio button. 		        |
|  			 15 		     |  			 selectcheckbox 		     |  			 Method 			to toggle a check box on/off  and to handle multiple sections. 		        |
|  			 16 		     |  			 findElement 		     |  			 It 			is If-else conditional action. If the element is present, then it 			will follow the actions in elementPresent Array. Else it will 			follow the actions in elementNotPresent array. 		              |
|  			 17 		     |  			 elementLooping 		     |  			 It 			will iterate certain process with respect to the value given. 		        |
|  			 18 		     |  			 scroll 		     |  			 It 			will scroll up/down/right/left the webpage. 		        |
|  			 19 		     |  			 typeText 		     |  			 It 			will enter the given data in the field where the cursor is 			presently located. 		           |
|  			 20 		     |  			 sendKey 		     |  			 It 			is similar to clicking on the Enter/TAB from current location. 			Enter or Tab name should be specified in sub action type. 		           |
|  			 21 		     |  			 clearText 		     |  			 It 			will clear the existing text in the field. 		        |
|  			 22 		     |  			 switchtoIframe 		     |  			 It 			will switch from one iframe to another 		        |
|  			 23 		     |  			 AcceptAlertWindow 		     |  			 It 			will click the OK button from the popup that appears. 		        |
|  			 24 		     |  			 Script 		     |  			 This 			action helps you to write your own java script. 		        |
|  			 25 		     |  			 Criteria 			Script 		        |  			 This 			action helps you to execute the java script based on specified 			criteria. 		           |



**Core Actions**

|  			 No 		     |  			 Action 			Name 		        |  			 Description 		     |
|-|-|-|
|  			 26 		     |  			 Screenshot 		     |  			 It 			will take the print screen of webpage. 		        |
|  			 27 		     |  			 Loop 		     |  			 It 			will execute a set of instruction repeatedly until some condition 			are fulfilled. 		           |
|  			 28 		     |  			 If 		     |  			 It 			will execute a set of instruction if a specified condition is 			true. 		           |
|  			 29 		     |  			 While 		     |  			 It 			will repeatedly execute a set of instruction until the given 			condition is true.  			 		              |
|  			 30 		     |  			 Display 			Message 		        |  			 It 			will display the predefined response message in UI after specific 			task was completed. 		           |
|  			 31 		     |  			 Set 			Variable 		        |  			 This 			action is used to set the value for already defined variable. 		        |
|  			 32 		     |  			 GUID 		     |  			 This 			action is used to set the value for already defined variable. 		        |
|  			 33 		     |  			 Create 			Datatable 		        |  			 This 			action is used to create a datatable during process execution 		        |


**MS office Plugin**

|  			 No 		     |  			 Action 			Type 		        |  			 Description 		     |
|-|-|-|
|  			 34 		     |  			 Read 			Data 		        |  			 Subcategory 			– word, it will fetch data from MS word file. 		        |
|  			 35 		     |  			 Write 			Range 		        |  			 Subcategory 			– excel, it will write data into MS Excel file. 		        |
|  			 36 		     |  			 Read 			Data – Cell Merge 		        |  			 It 			will merge the cells in MS excelsheet. 		        |
|  			 37 		     |  			 Read 			Data – Cell unmerge 		        |  			 It 			will unmerge all the merged cells in MS excelsheet. 		        |
|  			 38 		     |  			 Read 			Data – Read Cell 		        |  			 It 			will read the data from a specified cell. 		        |
|  			 39 		     |  			 Read 			Data – Read Row 		        |  			 It 			will read the data from a specified excel row. 		        |
|  			 40 		     |  			 Read 			Data – Read Column 		        |  			 It 			will read the data from a specified excel column. 		        |
|  			 41 		     |  			 Read 			Data – Read Column 		        |  			 It 			will read the data from the excel columns based on range 			specified. 		           |
|  			 42 		     |  			 Read 			Data – Read Range 		        |  			 It 			will read the data from the specified range from the excel sheet.  			  			 		              |

**Mail Plugin**

|  			 No 		     |  			 Action 			Type 		        |  			 Description 		     |
|-|-|-|
|  			 43 		     |  			 Get 			Mail 		        |  			 It 			is used to download file attachments from the email. 		        |
|  			 44 		     |  			 Send 			Mail 		        |  			 It 			is used to send mail (with/without attachments) to specific mail 			id. 		           |
|  			 45 		     |  			 Check 			Mail 		        |  			 It 			is used to check the mail based on the Subject text given. 		        |


**OCR Plugin**

|  			 No 		     |  			 Action 			Type 		        |  			 Description 		     |
|-|-|-|
|  			 46 		     |  			 Read 			Data 		        |  			 Subcategory 			- Abbyy Cloud 		        |
|  			 47 		     |  			 Read 			Data 		        |  			 Subcategory 			- Accura Scan 		        |


**PDF Plugin**

|  			 No 		     |  			 Action 			Type 		        |  			 Description 		     |
|-|-|-|
|  			 48 		     |  			 READ PDF DATA - Tesseract 		     |  			 It will fetch data from any image file. 		     |
|  			 49 		     |  			 READ PDF DATA - ITEXT 		     |  			 It will fetch data from clear and 			proper PDF file and it will not fetch data from scanned PDF. 		        |
|  			 50 		     |  			 READ PDF DATA – OCR space 		     |  			 It will fetch data from the PDF image 			that presents in live web URL. 		        |


Let us now see the actions in detail.

**4.1 UI Automation Plugin**: 

**OpenBrowser**

###### **JSON Format** ######

	"openBrowser":
	 {
		"referenceId":"M4CR-9FZW-5U8G-N2P3",
		"category": "Web UI Actions",
		"subCategory":"Selenium",
		"actionType": "OpenBrowser",
	   	"browserType": "chrome",
		"url": "https://www.gmail.com/",
		"scope": "ACTION"
	}

**wait**: It makes webdriver to wait for certain time before proceeding further in the code. 
We have used following three conditions for the wait action.

**a. Visibility wait**: will wait till the element appears. Maximum time out should be given in delayInMinutes parameter.

###### **JSON Format** ######

	 "Visibility_wait": {
	        "referenceId": "M4CR-9FZW-5U8G-N2P3",
	        "category": "Web UI Actions",
	        "subCategory": "Selenium",
	        "actiontype": "wait",
	        "executionType": "Driver",
	        "scope": "ACTION",
	       "selectType": "Condition",
	        "conditions": [{
	            "attr": "XPATH",
	            "value": "//*[@id=\"form1\"]/table/tbody//tbody/tr[1]/td/a",
	            "selectType": "VisibilityWait",
	            "delayInMinutes": "5",
	        }]
	    }

**b. LoadingMinutes**: will wait for default time of 2 seconds.

###### **JSON Format** ######

	 "LoadingMinutes": {
	        "referenceId": "M4CR-9FZW-5U8G-N2P3",
	        "category": "Web UI Actions",
	        "subCategory": "Selenium",
	        "actiontype": "wait",
	        "executionType": "Driver",
	        "scope": "ACTION",
	        "conditions": [{
	            "selectType": "LoadingMinutes"
	   }]
	   }

**c. isDocumentReady**: will wait till the last element get loads in the webpage.

###### **JSON Format** ######
 
	"IsDocument_Ready_Wait": {
	        "referenceId": "M4CR-9FZW-5U8G-N2P3",
	        "category": "Web UI Actions",
	        "subCategory": "Selenium",
	        "actiontype": "wait",
	        "scope": "ACTION",
	        "executionType": "Driver",
	        "conditions": [{
	            "selectType": "isDocumentReady"
	        }]
	    }

**setText**: It will set the value in a text input field.

###### **JSON Format** ######

	"setText":
	{ 
	        "referenceId": "M4CR-9FZW-5U8G-N2P3", 
	        "category": "Web UI Actions", 
	        "subCategory": "Selenium", 
	        "actiontype": "setText", 
	        "attr": "id", 
	        " applicantkey": "username", 
	        "value": "txtLoginUserName", 
	        "scope": "ACTION",
	        "executionType": "Driver" 
	}

**selectItem**: It will select one or multiple options from a dropdown list.

###### **JSON Format** ######

	"selectItem": { 
	        "referenceId": "M4CR-9FZW-5U8G-N2P3", 
	        "category": "Web UI Actions", 
	        "subCategory": "Selenium",
	        "actiontype": "selectItem", 
	        "attr": "XPATH", 
	        "applicantkeys": ["permitType"], 
	        "value": "html/body/form/select", 
	        "scope": "ACTION",
	        "executionType": "Driver" 
	}

**getText**: It will fetch data from the webpage and stored that data as a variable.

###### **JSON Format** ######

	"readAction":
	{ 
	        "referenceId": "M4CR-9FZW-5U8G-N2P3", 
	        "category": "Web UI Actions", 
	        "subCategory": "Selenium", 
	        "actiontype": "getText", 
	        "attr": "XPATH", 
	        "applicantkey": "content", 
	        "scope": "ACTION",
	        "value": "//*[@id=\"headingSubtext\"]/content", 
	        "executionType": "Driver" 
	}

**click**: It will click on the UI element with respect to the attribute given. It is same as the mouse left click on the required element.

###### **JSON Format** ######

	"buttonclick": 
	{ 
	        "referenceId": "M4CR-9FZW-5U8G-N2P3", 
	        "category": "Web UI Actions", 
	        "subCategory": "Selenium", 
	        "attr": "XPATH", 
	        "value": "//*[@id=\"LoginDiv\"]/div/div/input[2]", 
	        "actiontype": "click", 
	        "scope": "ACTION",
	        "executionType": "Driver" 
	}

**Hoverclick**: It will click on the mouse hover element.  It will trigger the base element first and then click on the hover element.

###### **JSON Format** ######

	"focusbuttonclick": 
	{ 
	        "referenceId": "M4CR-9FZW-5U8G-N2P3", 
	        "category": "Web UI Actions", 
	        "subCategory": "Selenium", 
	        "attr": "XPATH", 
	        "value": "html/body/form/table[3]/tbody/tr[2]/input", 
	        "actiontype": "Hoverclick", 
	        "scope": "ACTION",
	        "executionType": "Driver" 
	}  

**doubleClick**: It will double click on the UI element with respect to the attribute given. It is same as placing mouse pointer on the required element and clicking the mouse left button twice.

###### **JSON Format** ######

	"doubleclick": 
	{ 
	        "referenceId": "M4CR-9FZW-5U8G-N2P3", 
	        "category": "Web UI Actions", 
	        "subCategory": "Selenium", 
	        "attr": "XPATH", 
	        "value": "html/body/form/table[3]/tbody/tr[2]/input", 
	        "actiontype": "doubleClick", 
	        "scope": "ACTION",
	        "executionType": "Driver" 
	}

**hover**: It will move the mouse from its current position to the given offset (Horizontal and Vertical) position. It is similar to mouse hover on an element.

###### **JSON Format** ######

	"hover":  
	{  
	        "referenceId": "M4CR-9FZW-5U8G-N2P3",  
	        "category": "Web UI Actions",  
	        "subCategory": "Selenium",  
	        "attr": "XPATH",  
	        "value": "html/body/form/table/tbody/tr/td//tbody/tr/td[4]",         
	        "actiontype": "hover",  
	        "scope": "ACTION",
	        "executionType": "Driver"  
	}

**switchToWindow**: It will switch our focus control from one window to another window. Usually, it is used to switch over from main window to newly opened window.

###### **JSON Format** ######
  
	"windowswitch": 
	{ 
	        "referenceId": "M4CR-9FZW-5U8G-N2P3", 
	        "category": "Web UI Actions", 
	        "subCategory": "Selenium", 
	        "actiontype": "switchToWindow", 
	        "scope": "ACTION",
	        "value": "3", 
	        "executionType": "Driver" 
	}

**Enter**: It will press the enter key through selenium webdriver. It is similar to pressing the enter button in the keyboard.

###### **JSON Format** ######

	"ClickEnter":  
	{  
	         "referenceId": "M4CR-9FZW-5U8G-N2P3",  
	         "category": "Web UI Actions",  
	         "subCategory": "Selenium",  
	         "attr": "XPATH",  
	         "value": "html/body/form/table/tbody/tr/td//tbody/tr/td[4]",  
	         "actiontype": "Enter",  
	         "scope": "ACTION",
	         "executionType": "Driver"  
	 }

**focusEnter**: It will move on to the specific element and click on it.

###### **JSON Format** ######

	"FocusAndClickEnter": 
	{ 
	        "referenceId": "M4CR-9FZW-5U8G-N2P3", 
	        "category": "Web UI Actions", 
	        "subCategory": "Selenium", 
	        "attr": "XPATH", 
	         "scope": "ACTION",
	        "value": "html/body/form/table/tbody/tr/td//tbody/tr/td[4]", 
	        "actiontype": "focusEnter", 
	        "executionType": "Driver" 
	}

**NavigateElement**: It will move the focus from one element to another. It is similar to pressing the TAB button in keyboard.

###### **JSON Format** ######
	   
	"navigate_element":
	{ 
	        "referenceId": "M4CR-9FZW-5U8G-N2P3", 
	        "category": "Web UI Actions", 
	        "subCategory": "Selenium", 
	        "attr": "XPATH", 
	        "scope": "ACTION",
	        "value": "html/body/form/td[2]/input", 
	        "actiontype": "NavigateElement", 
	        "executionType": "Driver" 
	}

**selectradio**: Handles togging of radio button.

###### **JSON Format** ######

	"radio_button": 
	{ 
	        "referenceId": "M4CR-9FZW-5U8G-N2P3", 
	        "category": "Web UI Actions", 
	        "subCategory": "Selenium", 
	        "attr":"NAME", 
	        "value": "software", 
	        "actiontype": "selectradio", 
	        "executionType": "Script", 
	         "scope": "ACTION",
	        "selectType":"BYVALUE", 
	        "applicantkey":"Peachtree"         
	}

**selectcheckbox**: Method to toggle a check box on/off and to handle multiple sections.

###### **JSON Format** ######
   
	"check_box": 
	{ 
	        "referenceId": "M4CR-9FZW-5U8G-N2P3", 
	        "category": "Web UI Actions", 
	        "subCategory": "Selenium", 
	        "attr":"NAME", 
	        "value": "type", 
	         "scope": "ACTION",
	        "actiontype": "selectcheckbox", 
	        "executionType": "Script", 
	        "selectType":"BYVALUE", 
	        "applicantKeys":["notebook","netbook"]         
	}


**findElement**: It is If-else conditional action. If the element is present, then it will follow the actions in elementPresent Array. Else it will follow the actions in elementNotPresent array.

###### **JSON Format** ######

	  "find_element": { 
	        "referenceId": "M4CR-9FZW-5U8G-N2P3", 
	        "category": "Web UI Actions", 
	        "subCategory": "Selenium", 
	        "actiontype": "findElement", 
	        "executionType": "Driver", 
	        "attr": "XPATH", 
	        "value": "html/body/div[20]/div/div/div[2]/div[2]/div/input[@data-question=\"1\"]", 
	        "elementPresent": ["entercountry"], 
	        "elementNotPresent": ["entercolour"], 
	        "subfields": { 
	            "entercountry": { 
	                "attr": "XPATH", 
	                "applicantkey": "dubai", 
	                "value": "html/body/div[20]/div/div/div[2]/div[4]/div/input", 
	                "actiontype": "setText", 
	                "executionType": "Driver" 
	            }, 
	            "entercolour": { 
	                "attr": "XPATH", 
	                "applicantkey": "green", 
	                "value": "html/body/div[20]/div/div/div[2]/div[4]/div/input", 
	                "actiontype": "setText", 
	                "executionType": "Driver" 
	            } 
	        } 
	    }

**elementLooping**: It will iterate certain process with respect to the value given.

###### **JSON Format** ######

	"loopcheck": 
	{ 
	        "referenceId": "M4CR-9FZW-5U8G-N2P3", 
	        "category": "Web UI Actions", 
	        "subCategory": "Selenium", 
	        "executionType": "Driver", 
	        "actiontype": "elementLooping", 
	        "startIndex": "1", 
	        "indexName": "_indexesds", 
	        "value": "5", 
	        "actionList": ["newJob","windowhandleSleep"], 
	        "subfields": { 
	            "newJob": { 
	                "attr": "XPATH", 
	                "value": "//*[@id=\"Table3\"]/tbody/tr[2]/td[2]/table/tbody/
	                tr[_indexesds]/td[3]/a", 
	                "actiontype": "click", 
	                "executionType": "Driver" 
	            }, 

	            "windowhandleSleep": { 
	                "actiontype": "wait", 
	                "executionType": "Driver", 
	                "conditions": [{ 
	                "selectType": "LoadingMinutes" 
	                }] 
	            }    }     }

**Note:** The number of times the loop needs to iterated should be specified in “value” field.

1. If you want the value to be read from the documentgrid, then, you need to specify “attr” field as “documentGrid” and the variable name should be given in “value” field.

2. If you want the value to be determined by executing a script, then, you need to specify “attr” field as “script” and the variable name should be given in the “value” field.

**Scroll**: It will scroll up/down/right/left the webpage.

###### **JSON Format** ######

	 "Scroll": 
	{ 
	    "referenceId": "M4CR-9FZW-5U8G-N2P3", 
	    "category": "Web UI Actions", 
	    "subCategory": "Selenium", 
	    "executionType": "Script", 
	    "scope": "ACTION",
	    "actiontype": "scroll", 
	    "selectType": "up", 
	    "value": "500" 
	  }	 


**typeText**: It will enter the given data in the field where the cursor is presently located.

###### **JSON Format** ######

	 "type_text": 
	{ 
	        "referenceId": "M4CR-9FZW-5U8G-N2P3", 
	        "category": "Web UI Actions", 
	        "subCategory": "Selenium", 
	        "scope": "ACTION",
	        "actiontype":" typeText ", 
	        "applicantkey":"Hello world", 
	        "executionType": "Driver" 
	}

**sendKey**: It is similar to clicking on the Enter/TAB from current location. Enter or Tab name should be specified in sub action type.

###### **JSON Format** ######

	"sendkeys": 
		{ 
		     "referenceId": "M4CR-9FZW-5U8G-N2P3", 
		     "category": "Web UI Actions", 
		     "subCategory": "Selenium", 
		     "actiontype":"sendKey", 
		     "scope": "ACTION",
		     "subActiontype":"Tab",  
		     "executionType": "Driver" 
		}

**clearText**: 	It will clear the existing text in the field.

###### **JSON Format** ######
	 
	 "clear_text": {
	        "referenceId": "M4CR-9FZW-5U8G-N2P3",
	        "category": "Web UI Actions",
	        "subCategory": "Selenium",
	        "actiontype":"clearText",
	         "scope": "ACTION",
	        "attr": "XPATH",
	         "value": "//*[@id=\"Table3\"]/tbody/tr[2]/td[2]/table/tbody/tr[2]",
	        "executionType": "Driver"
	    }


**switchtoIframe**: It will switch from one iframe to another

###### **JSON Format** ######

	{
	        "switch_to_iframe": {
	        "attr": "id", 
	        "value": "txtLoginUserName", 
	        "actiontype": "switchToIframe", 
	        "executionType": "Driver",
	         "scope": "ACTION",
	        "subActiontype":"child" //child,parent,mostparent
	   }
	}


**acceptAlertWindow**: It will click the OK button from the popup that appears.

###### **JSON Format** ######

	 "alert": {
	        "referenceId": "M4CR-9FZW-5U8G-N2P3",
	        "category": "Web UI Actions",
	        "subCategory": "Selenium",
	        "actiontype": "acceptAlertWindow",
	        "scope": "ACTION",
	        "selectType": "accept",
	        "executionType": "Driver"
	}

**Script**: This action helps you to write your own java script.

###### **JSON Format** ######

	"readscript" : {
	             "referenceId": "M4CR-9FZW-5U8G-N2P3",
	             "category": "Web UI Actions",
	             "subCategory": "Selenium",
	             "actiontype":"script",
	             "executionType":"script",
	             "value":"<<Java_Script>>"
	}

**Criteria Script**: This action helps you to execute the java script based on specified criteria.

###### **JSON Format** ######

	"criteriascript": {
	        "referenceId": "M4CR-9FZW-5U8G-N2P3",
	        "category": "Web UI Actions",
	        "subCategory": "Selenium",
	        "actiontype": "criteriascript",
	        "executionType": "script",
	        "scope": "ACTION",
	        "criterias": [
	                        {
	                        "key":"${projectname}",
	                        "applicantkey": "@itemsTable.loopIndex.Project Name"
	                        }
	                    ],
	        "value": "var  pro  = '${projectname}'; 
	        var list = document.getElementsByClassName('r-table__tr'); 
	        for(i=1;i<list.length;i++)
	        { 
	        var dataNAME=document.querySelector('#main-dashboard-wrapper > 
	        div.item.click();
	        }
	       }"
	    }

**4.2 Core Actions**: 

**Screenshot**: It will take the print screen of webpage.

###### **JSON Format** ######

	 "screenshot":
	{
	"referenceId": "core",
	"category": "core",
	"actionType": "screenshot",
	"outPath": "$QM_HOME/$QM_OUTPUT_PATH",
	"value": "attachment"
	}

**Note:** “value” field contains the dataGrid key – to which the attachment downloaded path is stored.


**Loop**: It will execute a set of instruction repeatedly until some condition are fulfilled.

###### **JSON Format** ######

	"processLooping": {
	        "referenceId": "core",
	        "category": "core",
	        "actionType": "loop",
	        "loopIndex": 2,
	        "actionList": {
	            "login": {
	                "indexParam": 1,
	                "category": "ui_actions_plugin",
	                "scope": "GROUP",
	                "scriptPath": "/config_files/login.json"
	            },
	            "logout": {
	                "indexParam": 1,
	                "category": "ui_actions_plugin",
	                "scope": "GROUP",
	                "scriptPath": "/config_files/logout.json"
	            }
	        }
	    }


**If – Condition**: It will execute a set of instruction if a specified condition is true.

###### **JSON Format** ######

	 "if_condition": {
	    "referenceId": "core",
	    "category": "core",
	    "actionType": "if",
	    "condition": {
	    "operator": "equal",
	    "IdataType": "int",
	    "leftParam": "5",
	    "rightParam": "5",
	    "stateTrue": {
	    "process": {
	          "indexParam": 1,
	          "category": " ui_actions_plugin ",
	          "scope": "GROUP",
	          "scriptPath": "/config_files/login.json"
	        }
	      },
	      "stateFalse": {
	      "logout": {
	      "indexParam": 1,
	      "category": "ui_actions_plugin",
	      "scope": "GROUP",
	      "scriptPath": "/config_files/logout.json"
	        }
	      }
	    }
	  }


**While**: It will repeatedly execute a set of instruction until the given condition is true. 

###### **JSON Format** ######

	"whilecheck": {
	    "referenceId": "core",
	    "category": "core",
	    "actionType": "while",
	    "condition": {
	      "operator": "equal",
	      "calibrate": "increment",
	      "calibrationValue":1,
	      "startIndex": "0",
	      "endIndex": "3",
	      "continueTill": {
	        "process": {
	          "category": " ui_actions_plugin",
	          "scope": "GROUP",
	          "scriptPath": "/config_files/login.json"
	        }
	      }
	    }
	  }

**Display Message**: It will display the predefined response message in UI after specific task was completed.

###### **JSON Format** ######

	"message": 
	{
	        "referenceId": "core",
	        "category": "core",	
	        "actionType": "Display Message",
	        "message": ""
	}

**Set Variable**: This action is used to set the value for already defined variable.

###### **JSON Format** ######

	"setVariable": 
	{
	        "referenceId": "core",
	        "category": "core",
	        "actionType": "Set Variable",
	        "variableName":"",
	        "variableValue": ""
	}

**GUID**: This action is used to generate GUID.

###### **JSON Format** ######

	   "generate-id": {
	    "referenceId": "core",
	    "category": "core",
	    "subCategory": "Utils",
	    "actionType": "GUID",
	    "values": "ABCDEFGHabcdef0123456789",
	      "minlenght": 5,
	      "maxlenght": 10,
	      "documentGrid": "password",
	    "scope": "ACTION"
	  }

**Create Datatable**: This action is used to create datatable during process execution.

###### **JSON Format** ######

	"create_datatable":
	 {
	"referenceId": "core",
	"category": "core",
	"subCategory": "datatable",
	"actionType": "Create Datatable",
	"tableName": "dt1"
	},

	"add_header": 
	{
	"referenceId": "core",
	"category": "core",
	"subCategory": "datatable",
	"actionType": "Add Column Header",
	"tableName": "dt1",
	"columnHeaders": [
	"header1",
	"header2",
	"header3"
	],
	"columnTypes": [
	"String",
	"String",
	"String"
	]
	},
	"add_row": {
	"referenceId": "core",
	"category": "core",
	"subCategory": "datatable",
	"actionType": "Add Data Row",
	"tableName": "dt1",
	"rowValues": [
		"City",
		"State",
		"Postal Code"
	]
	}


**5. Plugin**

**5.1 MS office Plugin**

**Read Data**: It will fetch data from MS word file.
Here, you need to give Subcategory as word.

###### **JSON Format** ######

	{
	  "read": {
	    "referenceId":"E9D0-ZLTG-XKB4-UQHJ",
	     "category": "MsOffice Actions",
	    "subCategory":"Word",
	    "actionType": "Read Data",
	    "documentName": "path",
	    "fieldNames": [
	        {
	          "key": "DATE:",
	          "assignTo": "number"
	        },
	        {
	          "key": "INVOICE NO:",
	          "assignTo": "date"
	        },
	        {
	          "tableHeaders": [
	            "DESCRIPTION",
	            "QTY",
	            "UNIT PRICE",
	            "TOTAL"
	          ],
	          "assignTo": "itemsTable"
	        }
	      ]
	   }
	}


**Write Range**: It will write data into MS Excel file.
Here, you need to give Subcategory as excel.

###### **JSON Format** ######

	{
	"Write_to_excel": {
	    "referenceId": "E9D0-ZLTG-XKB4-UQHJ",
	    "category": "MsOffice Actions",
	    "subCategory":"Excel",
	    "actionType":"Write Range",
	    "dataTable": "itemsTable",
	    "sheetName": "items",
	    "startingCell": "A1",
	    "addHeaders": true,
	    "outPath": "$QM_HOME/$QM_OUTPUT_PATH/items.xlsx",
	    "copyPathTo": "path",
	    "scope":"ACTION"
	  }
	}


**Read Data – Cell Merge**: It will merge the cells in MS excelsheet.

###### **JSON Format** ######

	 {
	    "cell_merge": {
	        "referenceId": "E9D0-ZLTG-XKB4-UQHJ",
	        "category": "MsOffice Actions",
	        "subCategory": "Excel",
	        "actionType": "Read Data",
	        "documentName": "path",
	        "event": "Cell Merge",
	        "sheetName": "Page 1",
	        "range": "D6:F6"
	    }
	}

**Read Data – Unmerge cell**: It will unmerge all the merged cells in the sheet

	{
	    "read_excel": {
	        "referenceId": "E9D0-ZLTG-XKB4-UQHJ",
	        "category": "MsOffice Actions",
	        "subCategory": "Excel",
	        "actionType": "Read Data",
	        "documentName": "path",
	        "event": "Cell Unmerge",
	        "sheetName": "Page 1",
	        "range": "A:T"
	    }
	}

**Read Data – Read Cell**: It will read the data from a specified cell.

	{
	    "read_excel": {
	        "referenceId": "E9D0-ZLTG-XKB4-UQHJ",
	        "category": "MsOffice Actions",
	        "subCategory": "Excel",
	        "actionType": "Read Data",
	        "documentName": "path",
	        "event": "Read Cell",
	        "sheetName": "Page 1",
	        "cell":"A2",
	        "variable":"value"
	    }
	}

**Read Data – Read Row**: It will read the data from a specified excel row.

	{
	  "read_excel": {
	      "referenceId": "E9D0-ZLTG-XKB4-UQHJ",
	      "category": "MsOffice Actions",
	      "subCategory": "Excel",
	      "actionType": "Read Data",
	      "documentName": "path",
	      "event":"Read Row",
	      "sheetName":"test",
	      "addHeader": false,
	      "range":"A2:C2",
	      "assignTo":"itemsTable"
	  }
	}

**Read Data – Read Column**: It will read the data from a specified excel column

	{
	  "read_excel": {
	      "referenceId": "E9D0-ZLTG-XKB4-UQHJ",
	      "category": "MsOffice Actions",
	      "subCategory": "Excel",
	      "actionType": "Read Data",
	      "documentName": "path",
	      "event":"Read Column",
	      "sheetName":"test",
	      "addHeader": true,
	      "range":"D12:D16",
	      "assignTo":"itemsTable"
	  }
	}

**Read Data – Read Columns**: It will read the data from the specified excel columns

	{
	  "read_excel": {
	      "referenceId": "E9D0-ZLTG-XKB4-UQHJ",
	      "category": "MsOffice Actions",
	      "subCategory": "Excel",
	      "actionType": "Read Data",
	      "documentName": "path",
	      "event":"Read Columns",
	      "sheetName":"test",
	      "addHeader": true,
	      "range":"A:C",
	      "assignTo":"itemsTable"
	  }
	}


**Read Data – Read Range**: It will read the data from the specified range from the excel sheet.
 
	{
	  "read_excel": {
	      "referenceId": "E9D0-ZLTG-XKB4-UQHJ",
	      "category": "MsOffice Actions",
	      "subCategory": "Excel",
	      "actionType": "Read Data",
	      "documentName": "path",
	      "event":"Read Range",
	      "sheetName":"test",
	      "addHeader": true,
	      "range":"D12:E16",
	      "assignTo":"itemsTable"
	  }
	}

**5.2 Mail Plugin**

**GetMail**: This action is used to download file attachments from the email.

###### **JSON Format** ######

	 {
	  "Read_From_Mail_Server": {
	    "referenceId": "4WXR-BF1Q-3SMP-I6H5",
	    "category": "Mail Actions",
	    "subCategory": "POP3",
	    "actionType": "Get Mail",
	    "serverHost": "smtp.outlook.com",
	    "serverPort": 993,(server port)(995)
	    "mailProtocol": "imaps",(protocol)(pop3s)
	    "mailAuth": true,
	    "messageFolder": "inbox",(read mails from folder)
	    "messageStatus": "unread",(filter messages)
	    "messageSubject": "Test",(filter based on subject)
	    "mailFrom": "yourmailid@gmail.com",(filter based on mail from)
		"fileType": [".PDF"],
	    "getAttachments": true,
	    "markAsRead": true,
	    "outPath": "$QM_HOME/$QM_OUTPUT_PATH",(file will be download out files folder)
	    "userName": "username",
	    "password": "password",
	    "copyPathTo": "path",
	    "scope": "ACTION"
	  }
	}


**Send Mail**: It is used to send mail (with/without attachments) to specific mail id.

###### **JSON Format** ######

	{
	  "Send_Mail": {
	    "referenceId": "4WXR-BF1Q-3SMP-I6H5",
	    "category": "Mail Actions",
	    "subCategory": "SMTP",
	    "actionType": "Send Mail",
	    "serverHost": "smtp.outlook.com",
	    "serverPort": 587,
	    "mailProtocol": "smtp",
	    "mailAuth": true,
	    "starttlsEnable": true,
	    "sendAttachments": false,
	    "attachments": "#datagrid(attachment)",
	    "emailSubject": "Test QM Scheduler - Cron Testing-2",
	    "emailBody": "Hello world",
	    "templatePath": "resources/body.ftl",
	    "templateValues": { "mailcontent": "Bot Process Terminated" },
	    "sendTo": [ "yourmailid@gmail.com"],
	    "userName": "username",
	    "password": "password",
	    "scope": "ACTION"
	  }
	}

**Check Mail**: It is used to check the Mail based on the given Subject text.

###### **JSON Format** ######

	{
	  "Check_Mail": {
	    "referenceId": "4WXR-BF1Q-3SMP-I6H5",
	    "category": "Mail Actions",
	    "subCategory": "POP3",
	    "actionType": "Check Mail",
	    "serverHost": "smtp.outlook.com",
	    "serverPort": 993,(995)
	    "mailProtocol": "imaps",(pop3s)
	    "messageFolder": "inbox",
	    "messageStatus": "unread",
	    "mailAuth": true,
	    "starttlsEnable": true,
	    "userName": "username",
	    "password": "password",
	    "scope": "ACTION"
	  }
	}

**5.3 OCR Plugin**
**Read Data – Accura Scan**: It will fetch data from any image file.

###### **JSON Format** ######

	Subcategory - Accura Scan
	{
	  "Read_passport_data": {
	     "referenceId":"OECK-TQV1-2A4M-XB3F",
	     "category": "OCR Actions",
	     "subCategory":"Accura Scan",
	     "actionType": "Read Data",
	     "images":"path",
	     "cardType": "1",
	     "apiKey": "155376644211oeZPhrq60SeCNxpYAk01THJhCUFpuh7DpeK9mE",
	     "status": "status",
	     "name": "name",
	     "gender": "gender",
	     "passportNo": "passportNo",
	     "dob": "dob"
	    }
	}

**Read Data – Abbyy Cloud**: It will fetch data from an image.

###### **JSON Format** ######

	Subcategory – Abbyy Cloud

	{
	  "Read_passport_data": {
	      "referenceId":"OECK-TQV1-2A4M-XB3F",
	      "category": "OCR Actions",
	      "subCategory":"Abbyy Cloud",
	      "actionType": "Read Data",
	      "images":"path",
	      "mode":"MRZ",
	      "applicationId":"OCR_Abbyy_Process",
	      "password":"4nniBNGuHj0UsFMzZ42byNGc",
	      "name": "name",
	      "gender": "gender",
	      "passportNo": "passportNo",
	      "dob": "dob"
	   }
	}

**5.4 PDF Plugin**
**READ PDF DATA - Tesseract**: It will fetch data from any image file.

###### **JSON Format** ######

	{
	"Tesserect": {
	"referenceId": "OM9W-RV4L-HFTP-5UIY",
	"category": "PDF Actions",
	"subCategory": "TESSERECT",
	"actionType": "READ PDF DATA",
	"sourcePath": "E:\\POC\\FM POC\\FAM_POC_Scope_-_DCB_\\Cygnus tech.pdf", //local file path)
	"outputPath": "$QM_HOME/$QM_OUTPUT_PATH",
	"scope": "ACTION"
	    }
	}


**READ PDF DATA - ITEXT**: It will fetch data from clear and proper PDF file and it will not fetch data from scanned PDF.

###### **JSON Format** ######

	{
	"Itext": {
	"referenceId": "OM9W-RV4L-HFTP-5UIY",
	"category": "PDF Actions",
	"subCategory": "ITEXT",
	"actionType": "READ PDF DATA",
	"sourcePath": "E:\\test.pdf",(local pure PDF, not scan PDF)
	"outputPath": "$QM_HOME/$QM_OUTPUT_PATH",
	"scope": "ACTION"
	    }
	}
 
**READ PDF DATA – OCR space**: It will fetch data from the PDF image that presents in live web URL.

###### **JSON Format** ######

	 {
	"OCRSPACE": {
	"referenceId": "OM9W-RV4L-HFTP-5UIY",
	"category": "PDF Actions",
	"subCategory": "OCRSPACE",
	"actionType": "READ PDF DATA",
	"url": "https://5.imimg.com/data5/XZ/BJ/RJ/SELLER-92944351/pancard-500x500-500x500.jpg",
	 (live URL)
	"apikey": "89dd6120bd88957",
	"language": "eng",
	"outputPath": "$QM_HOME/$QM_OUTPUT_PATH",
	"isOverlayRequired": "false",
	"scope": "ACTION"
	}
	}

 

**5.5 Screen UI Plugin (for Desktop Applications)**

**Open Application**: Action will open the desktop application (Example: Calculator)

###### **JSON Format** ######

	"openApplication": 
	{
	"referenceId": "67VC-ZB25-N1GD-QYIU",
	"category": "UI Screen Actions",
	"subCategory": "AutoIt", 
	"actionType": "Open Application",
	"exePath": "C:\\Users\\calc.exe", // Location of the destop application (.exe file)
	"scope": "ACTION"
	}
 
**Click**: Action will perform click event

###### **JSON Format** ######

	 "click_password": {
	"referenceId": "67VC-ZB25-N1GD-QYIU",
	"category": "UI Screen Actions",
	"subCategory": "AutoIt",
	"actionType": "Click",
	"windowTitle": "Sign in", // Title of the page on which action to be performed.
	"windowLabel": "Sales - New Item", // optional, label value of the button.
	"locator": "Class", // value to find the element (Id or Class or xpath)
	"locatorValue": "WindowsForms10", // value of the locator
	"instance": "2", // If many number of elements present in a same class, in order 
	 to specify the respective element from the class, instance of the element to be provided.
	"scope": "ACTION"
	}
 
**Send Keys**: Action to perform send keys such as Ctrl + A, Tab, Enter, etc.

###### **JSON Format** ######

	 "sendKeys_enter": {
	      "referenceId": "67VC-ZB25-N1GD-QYIU",
	      "category": "UI Screen Actions",
	      "subCategory": "AutoIt",
	      "actionType": "Send Keys",
	      "keyValue": "Enter", // value of the key which should be performed.
	      "keyStrokeTimes": "2", // number of times the send key action need to be performed.  
	                                  (default: 1 time)
	      "scope": "ACTION"
	}
 
**Send Text**: Action to send the given text in the textbox

###### **JSON Format** ######

	 "sendText_description": {
	      "referenceId": "67VC-ZB25-N1GD-QYIU",
	      "category": "UI Screen Actions",
	      "subCategory": "AutoIt",
	      "actionType": "Send Text",
	      "dataGrid": "Your description", // value that needs to be entered in the textbox.
	      "scope": "ACTION"
	}
 
**Sleep**: Action to make the driver to sleep for specific time.

###### **JSON Format** ######

	 "sleep_30": {
	      "referenceId": "67VC-ZB25-N1GD-QYIU",
	      "category": "UI Screen Actions",
	      "subCategory": "AutoIt",
	      "actionType": "Sleep",
	      "delayInSecond": "2", // action will wait for the particular delay (in milliseconds)
	      "scope": "ACTION"
	}
 
**Close Window**: Action to close the window based on window title

###### **JSON Format** ######

	 "close_window": {
	      "referenceId": "67VC-ZB25-N1GD-QYIU",
	      "category": "UI Screen Actions",
	      "subCategory": "AutoIt",
	      "actionType": "Window Close", // Title of the window to be closed.
	      "windowTitle": "Login",
	      "scope": "ACTION"
	}

**Window Wait Active**: To wait until the window appears based on window title or window label in the expected window.

###### **JSON Format** ######

	 "WaitforWindowAppear": {
	"actionType": "Window Wait Active",
	"referenceId": "67VC-ZB25-N1GD-QYIU",
	"category": "UI Screen Actions",
	"subCategory": "AutoIt",
	"scope": "ACTION",
	"input": {
	"windowTitle": "", // Title of the window to which control to be switched.
	"windowLabel": "" // Any text in the window to which control to be switched.
		}
	}

**Get Text**: Action to extract text from the application 

###### **JSON Format** ######

	  "getItem": {
	      "referenceId": "67VC-ZB25-N1GD-QYIU",
	      "category": "UI Screen Actions",
	      "subCategory": "AutoIt",
	      "actionType": "Get Text",
	      "windowTitle": "AccountRight",
	      "windowLabel": "Sales - New Item",
	      "locator": "Class",
	      "locatorValue": "WindowsForms10 ",
	      "instance": "3",
	      "dataGrid": "extractedData", // To save the extracted data to a variable
	      "scope": "ACTION"
	}

**Mouse Click**: Action to perform mouse click using (x, y) coordinates.

###### **JSON Format** ######

	  "mouseClick": 
	{
	      "referenceId": "67VC-ZB25-N1GD-QYIU",
	      "category": "UI Screen Actions",
	      "subCategory": "AutoIt",
	      "actionType": "Mouse Click", 
	      "button": "left", // Mouse button click (left or right or middle)
	      "x": 898, // Coordinate of x-axis
	      "y": 470, // Coordinate of y-axis
	      "clicks": 1, // number of times the click action need to be performed
	      "scope": "ACTION"
	}

**Window Kill**: Action to kill specified window

###### **JSON Format** ######

	 "window_kill": {
	"actionType": "Window Kill",
	"referenceId": "67VC-ZB25-N1GD-QYIU",
	"category": "UI Screen Actions",
	"subCategory": "AutoIt",
	"scope": "ACTION",
	         "input": {
		"windowTitle": "", // Title of the window that need to be closed.
		" windowLabel ": "" // Any label text from the window that need to be closed 
		 	 	 	(Optional)
		}	
	}

**Window Active**: Action to Activate specified window

###### **JSON Format** ######

	 "stateTrue": 
	{	
	      "waitActive_Spelling": {
	      "referenceId": "67VC-ZB25-N1GD-QYIU",
	      "category": "UI Screen Actions",
	      "subCategory": "AutoIt",
	      "actionType": "Window Active", 
	      "windowTitle": "Spelling", // Title of the window to which control to be switched.
	      " windowLabel ": "", // Any text in the window to which control to be switched.
	        (Optional)
	      "scope": "ACTION"
	     }
	}

**Window Exists**: Action to check whether specified window exists or not

###### **JSON Format** ######

	 "isInformationExists_1": 
	{
	      "referenceId": "67VC-ZB25-N1GD-QYIU",
	      "category": "UI Screen Actions",
	      "subCategory": "AutoIt",
	      "actionType": "Window Exists",
	      "windowTitle": "Account Details ",
	      "windowLabel": "Information",
	      "dataGrid": "isInformationWindow",
	      "scope": "ACTION"
	}

**Get Window Title**: To get the title of specific window

###### **JSON Format** ######

	  "click_ok_1":
	 {
	      "referenceId": "67VC-ZB25-N1GD-QYIU",
	      "category": "UI Screen Actions",
	      "subCategory": "AutoIt",
	      "actionType": "Get Window Title",
	      "windowTitle": "Account Details",
	      "windowLabel": "Information",	
	      "locator": "Name",
	      "locatorValue": "btnLeft",
	      "scope": "ACTION"
	}

**Focus Input Field**: It will focus to the specific input field.

###### **JSON Format** ######

	  "focus_input_field": {
	       "actionType": "Focus Input Field",
	       "referenceId": "67VC-ZB25-N1GD-QYIU",
	       "category": "UI Screen Actions",
	       "subCategory": "AutoIt",
	       "scope": "ACTION",
	         "input": {
		"windowTitle": "", // Title of the window to which control to be switched.
		" windowLabel ": "", // Any text in the window to which control to be switched.  
	  	  	           (Optional)
	            "locator": "", // type of locator (xpath/id/css)
		"locatorValue": "", // value of the locator
	            "instance": "" // when there are many elements belongs a class name, then 
	             instance need to be given to specify the exact element.
	}
	}


**5.6 Print Action**

**Print**: This action helps developer to check whether the variable is assigned correctly or not. This action can be used after the step where variable is declared, so that developer can check the correct value is assigned as a variable.

###### **JSON Format** ######

	 "print":
	{
	      "referenceId": "IZAT-7ORE-JFK5-C86V",
	      "category": "Print Actions",
	      "actionType": "Print",
	      "printValue": "#runtimeinput(username)",
	      "scope": "ACTION"
	}




**5.7 Mobile Actions**

**establishConnection**: This action helps to establish Appium Server connection.

###### **JSON Format** ######

	 "startappium": {
	    "referenceId": "MOBI-PMJC-WF1V-O9EP",
	    "category": "Mobile Actions",
	    "subCategory": "appium",
	    "actionType": "establishConnection",
	    "desiredCapablities": [
	      "browserName: ", // Name of the mobile web browser to automate. Should be 
	       empty string if automating an app instead
	       "platformVersion:4.4.2", // Version name you mobile operating system (Andorid, 
	       	IOS, or Windows)      
	      "deviceName:Lenovo TAB 2", // Name of the mobile device to use
	      "platformName:Android", // Name of the mobile OS
	      "appPackage:com.truecaller", // Package of the Android app you want to run the 
	       automation process
	      "appActivity:com.truecaller.ui.TruecallerInit" // Name of the android activity 
	       you want to launch from package
	    ],
	    "url": "http://127.0.0.1:4723/wd/hub", // Url of the appium server
	    "scope": "ACTION"
	  }

**visibilityWait**: It is an explicit wait which will wait till some pre built condition become true. Eg. Wait for elements to become clickable, visible, invisible, etc. Maximum time out should be given in timeOutSeconds parameter.

###### **JSON Format** ######

	"visiblitywait": {
	    "referenceId": "MOBI-PMJC-WF1V-O9EP",
	    "category": "Mobile Actions",
	    "subCategory": "appium",
	    "actionType": "visiblityWait",
	    "attr": "id", // Type of the attribute (attributes can be id/xpath/class)
	    "value": "com.truecaller:id/nextButton", // This action will wait 
	     till this element appears.
	    "timeOutSeconds": 15, // Maximum wait time
	    "scope": "ACTION"
	  }


**elementVisiblityCheck**: Action to click on the element.

###### **JSON Format** ######

	"alertpresentornot2": {
	"referenceId": "MOBI-PMJC-WF1V-O9EP",
	"category": "Mobile Actions",
	"subCategory": "appium",
	"actionType": "elementVisiblityCheck",
	"attr": "id",
	"value": "com.truecaller:id/empty_state_logo",
	"out": "alertcheck",
	"scope": "ACTION"
	 }

**click**: Action to click on the element.

###### **JSON Format** ######

	   "clicknotification1": {
	    "referenceId": "MOBI-PMJC-WF1V-O9EP",
	    "category": "Mobile Actions",
	    "subCategory": "appium",
	    "actionType": "click",
	    "attr": "driverId", // Type of the attribute, it can be id/xpath/class/driverId/
	     driverxpath/driverClassName/driverAccessibilityId
	    "value": "com.truecaller:id/nextButton",
	    "scope": "ACTION"
	  }

**touchAction**: Action to interact with an element on mobile touchscreen through x and y axis.

###### **JSON Format** ######

	    "touchaction1": {
	              "referenceId": "MOBI-PMJC-WF1V-O9EP",
	              "category": "Mobile Actions",
	              "subCategory": "appium",
	              "actionType": "touchAction",
	              "xaxis": 200, // Touch-driven panning is permitted along the x-axis.
	              "yaxis": 200, // Touch-driven panning is permitted along the y-axis.
	              "scope": "ACTION"
	 }

**sendKeys**: It will enter the given data in the field.

###### **JSON Format** ######

	       "entermobile":
	 {
	              "referenceId": "MOBI-PMJC-WF1V-O9EP",
	              "category": "Mobile Actions",
	              "subCategory": "appium",
	              "actionType": "sendKeys",
	              "arguments": "@LocationDetail.loopIndex.Mobile",
	              "attr": "driverClassName",
	              "value": "android.widget.EditText",
	              "scope": "ACTION"
	  }


**getText**: It will retrieve the inner text of the element that present in between opening and closing tags. It will store the value as variable that given as “out”.

###### **JSON Format** ######

	"getName": {
	              "referenceId": "MOBI-PMJC-WF1V-O9EP",
	              "category": "Mobile Actions",
	              "subCategory": "appium",
	              "actionType": "getText",
	              "attr": "className",
	              "value": "android.widget.TextView",
	              "instance": "0",
	              "out": "NameOfPerson",
	              "notFound": "not present", // When there is no text in the location, 
	               then the value will be assigned as “not present”.
	              "scope": "ACTION"
	            }