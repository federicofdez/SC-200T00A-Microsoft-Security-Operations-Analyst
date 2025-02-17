# Module 6 - Lab 1 - Exercise 2 - Connect Windows devices to Azure Sentinel using data connectors

### Task 1: Create a Windows Virtual Machine in Azure.

In this task, you will create a Windows virtual machine in Azure.

1. Login to WIN1 virtual machine as Admin with the password: **Pa55w.rd**.  

2. In the Edge browser, navigate to the Azure portal at https://portal.azure.com.

3. In the **Sign in** dialog box, copy, and paste in the **Tenant Email** account provided by your lab hosting provider and then select **Next**.

4. In the **Enter password** dialog box, copy, and paste in the **Tenant Password** provided by your lab hosting provider and then select **Sign in**.

5. Select **+ Create a Resource**.

6. In the **search services and marketplace** box, enter *Windows 10*. 

7. Select the **Create** dropdown for *Microsoft Windows 10*.  Then select **Windows 10 Enterprise, version 20H2**.

8. Select your Subscription.

9. Create a new Resource Group named **rg-AZWIN01** if you have not done so already.

**Note:** This should be a new resource group for tracking purposes.  

10. Set the Virtual machine name to AZWIN01.

11. Set the Region to the appropriate region for your area.  The appropriate region will probably default.

12. Enter a Username of your choosing that is acceptable for Azure.

13. Enter a Password of your choosing. 

**Hint:** It might be easiest to use your tenant password.

14. Select the Licensing confirmation.

15. Select **Review + create**.

16. Select **Create**. Wait for the Resource to be created, this may take a few minutes.

### Task 2: Connect an Azure Windows virtual machine.

In this task, you will connect an Azure Windows virtual machine to Azure Sentinel.

1. In the Search bar of the Azure portal, type *Sentinel*, then select **Azure Sentinel**.

2. Select your Azure Sentinel Workspace you created earlier.

3. From the Data Connectors Tab, select the **Security Events** connector from the list.

4. Select your Azure Sentinel Workspace if prompted.

5. Select **Open connector page** on the connector information blade.

6. Select the **Install agent on Azure Windows Virtual Machine** option.

7. Select **Download & install agent for Azure Windows Virtual machines**.

8. Select the **AZWIN01** virtual machine in the list that you just created in the previous task, then select **Connect**. Wait until the *connecting...* message disappears.

9. Select **Virtual machines** in the navigation list. You should now see the virtual machine has a Log Analytics Connection.

### Task 3: Connect a non-Azure Windows Machine.

In this task, you will connect a non-Azure Windows virtual machine to Azure Sentinel.

1. Login to WIN2 virtual machine as Admin with the password: **Pa55w.rd**.  

2. Open the Microsoft Edge browser.

3. Open a browser and log into the Azure Portal at https://portal.azure.com with the credentials you've been using in the previous labs.

4. In the Search bar of the Azure Portal, type *Sentinel*, then select **Azure Sentinel**.

5. Select your Azure Sentinel Workspace.

6. Select **Data connectors** then select the **Security Events** connector from the list.

7. Select **Open connector page** on the connector information blade.

8. In the Select which events to stream area, select **All Events**, then select **Apply Changes**.

9. Select the **Install agent on a non-Azure Windows Machine**.

10. Select **Download & install agent for non-Azure Windows machines**. 

11. Select the link for **Download Windows Agent (64 bit)**.

12. Run the .exe file that is downloaded and confirm the User Account Control prompt that may appear.

13. Select **Next** on the Welcome dialog.

14. Select **I Agree** on the Microsoft Software License Terms page.  On the Destination prompt select **Next**.

15. On the Agent Setup Options prompt, select **Connect the agent to Azure Log Analytics (OMS)** option, then select **Next**.

16. In the browser with Azure Sentinel open, copy the **Workspace ID** from the Agents Management page and paste into the Workspace ID in the dialog. 

17. In the browser with Azure Sentinel open, copy the **Primary key** from the Agents Management page and paste into the Workspace key in the dialog. 

18. Select **Next**.

19. Select **Next** on the Microsoft Update page.

20. Then select **Install**.  When complete select **Finish**.

### Task 4: Install and collect Sysmon logs.

In this task, you will install and collect Sysmon logs.

You should still be connected to the WIN2 virtual machine.  The following instructions will install Sysmon with the default configuration.  You should research community based configurations for Sysmon to be used on production machines.

1. In the browser, go to https://docs.microsoft.com/sysinternals/downloads/sysmon

2. Download Sysmon from the page by selecting **Download Sysmon**.

3. Open the downloaded file and extract the files to a new directory c:\sysmon

4. In the Windows Taskbar for WIN2 search box, enter *command*.  The search results will show Command Prompt app.  Right-click on the Command Prompt app and select **Run as Administrator**.  Confirm any User Account Control prompts that appear.

5. Enter *cd \sysmon*

6. Type *notepad sysmon.xml* to create a new file.

7. Open a tab in the browser and navigate to: https://github.com/SwiftOnSecurity/sysmon-config/blob/master/sysmonconfig-export.xml

8. Select the **Raw** button and copy the contents of that file from Github to the sysmon.xml notepad file you just create and **save** the file.

9. In the command prompt type the following and press enter:
    sysmon.exe -accepteula -i sysmon.xml

**Note:**  Verify that "Configuration file validated" and "Sysmon started" messages appear in the output.

10. In the browser, navigate to the Azure portal at https://portal.azure.com 

11. In the Search bar of the Azure portal, type *Sentinel*, then select **Azure Sentinel**.

12. In Azure Sentinel, select **Settings** from the Configuration area and then select **Workspace settings >** tab.

13. Make sure your Azure Sentinel Workspace is selected.

14. Select **Agents configuration** from the Settings area.

15. Select the **Windows Event logs** tab.

16. Select **Add windows event log** button.

17. Type **Microsoft-Windows-Sysmon/Operational** in the Log name field.

18. Select **Apply**.

### Task 5: Onboard Microsoft Defender for Endpoint Device.

In this task, you will on-board a device to Microsoft Defender for Endpoint.

**Note:** If you completed the labs in the first module of this course AND saved your Virtual Machines you have already performed this task.  If you’re using the same virtual machine from that lab exercise you can skip this task.

1. Login to WIN1 virtual machine as Admin with the password: **Pa55w.rd**.  

2. In the Edge browser, go to the Microsoft 365 Defender portal at (https://security.microsoft.com) and login with the **Tenant Email** credentials if you are not currently in the portal.

3. Select **Settings** from the left menu bar, then from the Settings page select **Endpoints**.

4. Select **Onboarding** in the Device management section.

5. Select **Download Package**.

6. Extract the downloaded .zip file.

7. Run the Windows Command Prompt as **Administrator** and agree to any User Account Control prompts that appear.

8. Run the WindowsDefenderATPLocalOnboardingScript.cmd file that you just extracted as administrator. **Note** By default the file should be in the c:\users\admin\downloads directory. Answer Y to questions presented by the script. 

9. From the Onboarding page in the portal, copy the detection test script and run it in an open command window.  You may have to open a new **Administrator: Command Prompt** window by typing *CMD* in the windows search bar and choose to **run as Administrator**.

10. In the Microsoft 365 Defender portal in the Endpoints area, select **Device inventory**. You should now see your device in the list.

## Proceed to Exercise 3
