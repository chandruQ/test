---
id: doc6
title: Qruize Magic - Help Document for Creating Plugins
sidebar_label: How to Develop a Custom Plugin?
---


<!DOCTYPE html>
<html>
   <head>
      <title>HTML Backgorund Color</title>
      <body style="background-color:;">



## <u>Prerequisite :</u> ##

Installation of JAVA 14 and set environmental variable path

(To check Java has already installed in your system, in command prompt window, type java –version and press the enter key. It will display you the java version if it is already installed). 

To install JAVA 14 in your windows system (64-bit), open the URL
**https://www.oracle.com/java/technologies/javase/jdk14-archive-downloads.html**

Click on the link shown below to download the Java package. Run the .exe file and do the installation process.

![Java Download model](/img/PluginDevelop/1.jpg)


**To set environmental path for Java JDK file**

a) To set Java JDK path on User variable, provide JAVA_HOME as variable name

b) Set extracted base path up to jdk-14.0.1 as Variable value. 
For example: C:\Program Files\Java\jdk-14.0.1

![Java environment](/img/PluginDevelop/2.jpg)


**Setting environmental variable path for java JDK bin folder**

c) To set Java path on system variable, double click on Path and set extracted base path up to bin folder as Variable value. Then click on the OK button.

![Java bin model](/img/PluginDevelop/3.jpg)

**Install Eclipse Oxygen (Eclipse IDE for Java EE Developers – 64 bit) from the below link 
https://www.eclipse.org/downloads/packages/release/oxygen/3a/eclipse-ide-java-ee-developers**

![Eclipse Download model](/img/PluginDevelop/4.jpg)

Download all the below files that require for creating QruizeMagic plugins - **QruizeMagic.zip**

**https://qruizemail.sharepoint.com/sites/qruizemagic/Shared%20Documents/QruizeMagic%20Setup%20file%20and%20document/QruizeMagic.zip**

### Reference files ###

SampleProcess
**https://qruizemail.sharepoint.com/:u:/s/qruizemagic/EddqRVXFhL5GjOMivAh1vG8B1fcirIUrHz6aIAc1hAPdnA?e=rbKiiu**

template_sample or sample plugin
**https://qruizemail.sharepoint.com/:u:/s/qruizemagic/EYUT7L4Euq5MjOWsOkukE1MBkqcOSgpTKDcjS219uCG18Q?e=sgdyDC**

Fully Developed Plugin Sample
**https://qruizemail.sharepoint.com/:u:/s/qruizemagic/EYzOyMBl-4lJomCga--YQjgBqy4pPDxcz9nrvWQPOxNKIw?e=aw7faX**

## <u>Steps Involved in Creating Plugin</u> ##

#### Example 1: ####

Here we are going to create a plugin (sampleProcess) which is used to print a string “HelloWorld” in a command prompt window. 
1. Extract the QruizeMagic.zip file and save it in C or D drive and unzip it. 

Setting environmental variable path for QruizeMagic:

a) In the windows search field, type “Edit the System Environmental variables” and click on the enter button,

b) Click on the Environmental Variables… button in the Advanced tab,

c) In the user variables section, click on the New button,

d) To set QM application path on User variable, provide QM_HOME as variable name,

e) Set extracted base path up to QruizeMagic as Variable value.

For example: C:\Users\kannan\Desktop\22.07.19\QruizeMagic

f) Click on the OK button.

![Java QM home model](/img/PluginDevelop/5.jpg)

2. Open Eclipse and import plugin file (Eg. template)

![Plugin import model](/img/PluginDevelop/6.jpg)

3. Open pom.xml and enter Artifact id and Name (Here it is HelloWorld).

![POM xml model](/img/PluginDevelop/7.jpg)

4. Click on src/main/resources package and open plugin.properties file
5. plugin.name should be same as artifact id and name given in the pom.xml. Fill the plugin id, class, name, and version details. plugin id should be unique.

![plugin id model](/img/PluginDevelop/8.jpg)

6. Click on src/main/java package and open com.qruize.template.plugin file 
7. Open PluginTemplate.java file and scroll down to **execute()** method. At the beginning, PluginTemplate.java will be initiated and the program execution for the plugin takes place.
8. To link your process, you need to call the specific process method in the execute method. Here SampleService is a class name and execute is the process method.

  **Example:**

    @Override

	public void execute() throws Exception 
     {
	   new SampleService().execute(robotContext);
     }
9. Since the process are being created using JSON, make sure the JSON file contains valid data. So that the plugin can interpret with JSON file and perform suitable action.

![JSon model](/img/PluginDevelop/9.jpg)

10. To perform data communication between plugins, we are using **Variables.java** file. 
Here the value1 can be used in various plugins. Open **Variables.java** file and assign value1 as **‘HelloWorld’** and then save the file.

![Variable model](/img/PluginDevelop/10.jpg)

11. The variable name given in JSON file (value1) will get assigned in this valueForm string of the **SampleEntity.java** file.

![SampleEntity model](/img/PluginDevelop/11.jpg)

12. Open **SampleService.java** file. Now assign the value to valueFrom variable.

![valueFrom model](/img/PluginDevelop/12.jpg)

13. To build the plugin zip file, right click on sample.actions > Run as > Maven build. The Edit Configuration popup will appear. In the Goals field type **‘clean install’**   and click on the Run button.

![Configuration model](/img/PluginDevelop/13.jpg)

14. To view the newly created plugin file, right click on sample.actions > Show In > System Explorer. Now it will move on to the template folder location. Open the template folder and then open the target folder. You can now find the plugin build (in this case it is **HelloWorld-v1.0.0.1.zip** file).
15. Copy the plugin zip folder (Build) in the respective path **\QruizeMagic\.qm\HelloWorld\v1.0.0.1**
16. Open process folder and then open newly created process folder. Open the profile.json file and update the plugin name.

![plugin name model](/img/PluginDevelop/14.jpg)

17. Run the command to execute the QruizeMagic jar files.
18. Executing process from postman 
Endpoint: **http://localhost:9090/v1/api/automation/<<process_name>>/<<robot-key>>/<<process-version>>/automate** 

Now you can see the output **‘HelloWorld’** in the command window.

![process model](/img/PluginDevelop/15.jpg)

#### Example 2: ####

In this example, we are going to create a plugin (TwoActionsOnePlugin) which is used to get a string value and print it in the command prompt window. 
1. Open Eclipse
2. Import plugin file (Eg. template)

![Import plugin model](/img/PluginDevelop/16.jpg)

3. Open **pom.xml, enter Artifact id and Name** (Here it is TwoActionsOnePlugin).

![OnePlugin model](/img/PluginDevelop/17.jpg)

4. Click on src/main/resources package and open plugin.properties file
5. plugin.name should be same as artifact id and name given in the pom.xml. Fill the plugin id, class, name, and version details. plugin id should be unique.

![plugin id model](/img/PluginDevelop/18.jpg)

6. Create a **Constants.java** file and type the lines as shown below. Here we are declaring two variables read and write and assigning its value for READ and WRITE respectively.

![WRITE model](/img/PluginDevelop/19.jpg)

7. Create Entity files (Here it is MyEntity and MyEntity2) and type the code as shown below. This file will convert the values given in JSON to an Object. The variable name given in JSON file (value1 and value2) will get assigned in this valueForm string of the **SampleEntity.java** file.

![MyEntity model](/img/PluginDevelop/20.jpg)

![MyEntity2 model](/img/PluginDevelop/21.jpg)

8. Click on src/main/java package and open com.qruize.template.plugin file. Open PluginTemplate.java file and scroll down to **execute()** method. At the beginning, PluginTemplate.java will be initiated and the program execution for the plugin takes place.

![PluginTemplate model](/img/PluginDevelop/22.jpg)

   In the above Blue highlighted code, we are differentiating two actions (READ and WRITE) by creating a new field action type in JSON. 

   Here the **execute()** method will get the action type from the JSON and redirecting the execution to that specific action class.

9. We are going to add two different actions in a plugin, we need to add two different classes SampleService and SampleService2. To link your process, you need to call the specific process method in the execute method. 

#### Sample Service ####

Open **SampleService.java** file. Now assign the value to valueFrom variable.

![SampleService model](/img/PluginDevelop/23.jpg)

#### Sample Service2 ####

![SampleService2 model](/img/PluginDevelop/24.jpg)

10. Open the **Variable.java** file in the variable folder and declare the string value to test (Variable).

![Variable model](/img/PluginDevelop/25.jpg)

11. Since the process are being created using JSON, make sure the JSON file contains valid data. So that the plugin can interpret with JSON file and perform suitable actions (read and write). Here the variable test given inside the datagrid and Welcome to Plugin Creation will be copied to list variable. Then these string values will get printed in the command prompt window.

![(read and write model](/img/PluginDevelop/26.jpg)

12. To build the plugin zip file, right click on sample.actions > Run as > Maven build. The Edit Configuration popup will appear. In the Goals field type ‘clean install’ and click on the Run button.

![clean install model](/img/PluginDevelop/27.jpg)

13. To view the newly created plugin file, right click on TwoActionsOnePlugin > Show In > System Explorer. Now it will move on to the template folder location. Open the template folder and then open the target folder. You can now find the plugin build (in this case it is TwoActionsOnePlugin-v1.0.0.1.zip file).
14. Copy the plugin zip folder (Build) in the respective path **\QruizeMagic\.qm\TwoActionsOnePlugin\v1.0.0.1**
15.  Open process folder and then open newly created process folder. Open the profile.json file and update the plugin name.

![TwoActionsOne model](/img/PluginDevelop/28.jpg)

16. Run the command to execute the QruizeMagic jar files.
17. Executing process from postman 
Endpoint: **http://localhost:9090/v1/api/automation/<<process_name>>/<<robot-key>>/<<process-version>>/automate**
Now you can see the string value output in the command window.

![command model](/img/PluginDevelop/29.jpg)

