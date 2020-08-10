---
id: doc4
title: Qruize Magic - Sample Process
sidebar_label: How to Run Sample Process?
---




1. **Introduction**
The purpose of this document is to describe you the steps involved for executing the process using Qruize Magic application. 

2. **Document Scope and Intended Audience**
This run document is intended to be used by software support personnel who will be responsible for planning, performing, or maintaining the process execution of the application.

3. **Getting Started – Major steps involved in executing Process using Qruize Magic**

	a. Open the Qruize Magic web application and login as a TENANT ADMIN.

	b. Create a new process and upload the process (.zip) file.

	c. Map the user with that process and click on the Bundle and Submit button.

	d. Map the agent to the process, map the BOT to the process, and then publish the process.

	e. Run the BOT command in command prompt window.

	f. Switch over to the Agent role

	g. Upload the file that involves process execution and click on the BEGIN button to initiate the process automation.

	h. View the execution result in the results page.












4. **Steps involved in executing Process using Qruize Magic**

   **Tenant Admin Login**

   Step 1: Open the Qruize Magic application. Enter the valid username and password and then click on the **LOGIN button**.

   ![Login screen](/img/Runsample/1.jpg)

   Step 2: To create a new process, click on the **TENANT ADMIN** button in order to proceed with tenant admin role.  

   ![Tenant screen](/img/Runsample/2.jpg)

   Step 3: To add a new process, select New Process from the Process Management dropdown.

   ![Process screen](/img/Runsample/3.jpg)

   Step 4: In the Add Process page, enter the process name, description and map the process to the project (if required). Select the **“Do you want upload Process file?”** check box and upload the process zip file.

   ![Add process](/img/Runsample/4.jpg)

   Step 5: To map the user with the newly created process, select the user from the User dropdown and click on the ADD USER button. Select the privilege(s) for the user by selecting the respective checkboxes. Then click on the BUNDLE & SUBMIT button.

   ![Bundle Submit](/img/Runsample/5.jpg)

   Step 6: The Process file will be now moved to the **BUNDLED** section. The process can be executed only when it is published. So, click on the **PUBLISH** button. 

   ![Publish screen](/img/Runsample/6.jpg)

   Step 7: First we need to map the agent to the process and then map the BOT to the process. Here we have mapped the process with the existing bot. So that the process can be only executed through the BOT mapped with it. 
	To execute the process using your authorized credentials, you can provide your details in USERNAME and PASSWORD fields which is assigned as the **"run time input parameter"** for BOT execution. For an agent, it is possible to map multiple bots for a single process. Here you can provide separate credentials as run time input parameter.

	![Process map](/img/Runsample/7.jpg)

   Click on the PUBLISH button to publish the process.
   Now the Published process is listed out. 

   ![My process screen](/img/Runsample/8.jpg)
 
   Fork Process will help you to replace the old process zip file with the new one. Once you click the CONFIRM button, the process gets forked and listed under the CONSTRUCTION menu. Click on the edit icon to upload the updated process zip file, bundle it, and then publish it. 

   ![Fork screen](/img/Runsample/9.jpg)

   Step 8: If you want map the process with a new bot, you need to create a new bot. To do this, click on the Process Management tab and select Bot List from the dropdown menu. In the page that appears click on the ADD BOT button. Now the Add BOT page will appear.

   ![Add BOT](/img/Runsample/10.jpg)

   After entering BOT name and description details, select BOT Type as “Standard” and SUB BOT Type as “Floating”. Then click on the ADD button. 

   Now the BOT is created and listed as shown below. Note down the BOT key.

   ![BOT List](/img/Runsample/11.jpg)

    Step 9: **Initiate the BOT.**

    ![Initiate BOT](/img/Runsample/12.jpg)


**Agent Login**

   Step 1: You will receive a mail provided with login credentials for Agent role and a BOT key. Now login to the Qruize Magic application as an **Agent**. 

![Agent login](/img/Runsample/13.jpg)


   Select **Bot Configuration** tab. In the **BOT License Key** field, paste the BOT key which was generated during the BOT creation using Tenant Admin. Click on the **CONFIGURE** button. 
 
![BOT Config](/img/Runsample/14.jpg)

   Step 2: To execute the RPA, select **My Process** tab at the top, the list of process will appear. Click on the **EXECUTE** button of the process you want to execute.
 
![Agent Process](/img/Runsample/15.jpg)

   Step 3: Now the **Execute Process** page will appear. Map the BOT which was created by Tenant Admin. Once the BOT is selected, the RUN TIME OPTIONS section will be enabled along with USERNAME and PASSWORD.
   
   In the RUNTIME INPUT ARGUMENTS section, enter the Excel password and click on the Upload button to upload the excel file. Click on the **BEGIN** button to execute the process automation.  

![Execute process](/img/Runsample/16.jpg)

   Step 4: Once the execution is completed, you can see the result status by clicking on the **Results** tab. The process execution result will be listed along with start and end time. You can view the log details by clicking on the **info** icon.

![Tenant screen](/img/Runsample/17.jpg)


   5. **Conclusion**
    This document covers the steps for uploading and executing process on Qruize Magic application. This document will be enhanced to add more required technology components and release in various document versions.


**<u>Disclaimer</u>**:
No part of this document can be reproduced, transferred, distributed or stored in any format without the prior written permission from Qruize Technologies Pvt. Ltd.


