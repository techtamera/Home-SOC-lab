# Home-SOC-lab
DESCRIPTION
-

An azure honeypot in which intentional access is given to the public internet in order to allow the machine to be attacked. Using Microsoft Sentinel, we track the failed login attempts from the log repository that we configured and connected to the SIEM. Lastly, an attack map was created using the data collected from the SIEM.
-
TECHNOLOGY UTILIZED
-

- Azure Virtual Machine
- Microsoft Sentinel (SIEM)
- KQL
----

Azure Virtual Machine Setup Steps
-

In order to begin creating the virtual machine, you will have to have an azure subscription. You can access the website to create your subscription at www.azure.microsoft.com. Once your subscription has been created, You will then be able to log into the azure portal at www.portal.azure.com. Once that is done, you will need to create a resource gorup. Type resource group into the search box and click on "resource group". This will bring you to a page that looks like this:

<img width="1464" height="792" alt="Screenshot 2025-11-18 at 6 57 02 PM" src="https://github.com/user-attachments/assets/d827a246-6aa5-4227-94a3-0f6882703530" />

Press the "Create" button in order to create the resource group. (Creating a resource group is important because it allows us to logically bundle related resources and tools together into one container. This gives us the capability to easily manage and deploy Azure resources). After clicking on create, you will create the resource group name and select the region. 
<img width="1454" height="721" alt="Screenshot 2025-11-18 at 6 58 36 PM" src="https://github.com/user-attachments/assets/38768ca6-7c73-4d33-8e49-676b37a9e99f" />

Press Review+Create. After the resource group is created, we will then create the virtual network. Type "virtual network" in the search box and click on virtual network. Then click "create virtual network". Ensure that you choose the resource group that we just created and ensure that the region of choice is the same as the region we chose for the resource group we previously created. Create a name for the virtual network. Your virtual network page should look something like this:

<img width="1450" height="721" alt="Screenshot 2025-11-18 at 7 04 34 PM" src="https://github.com/user-attachments/assets/d7a16bfc-b638-4276-9caa-580fc2594f3d" />

Press Review+Create. After the virtual network is created, we will then create the virtual machine. Type "virtual machine" into the search box and click on virtual machine. Then click "create". 

<img width="1448" height="725" alt="Screenshot 2025-11-18 at 7 10 08 PM" src="https://github.com/user-attachments/assets/94929b82-d88e-4967-91e9-94f34336663c" />

Ensure that you chose the correct resource group. Create a name for the virtual machine. Choose the same region as the region for the resource group. Choose the image and size that you want to create the Virtual machine. Create a username and password (this will be the login that you will use to sign into the virtual machine using RDP). You will then click next for disks which you will leave as is. Then click next for networking. You will choose the virtual network that we just created from the virtual network drop down box. Then you will choose the default subnet option from the subnet drop down box and then check the box to delete public IP and NIC. Click next for management which you will leave as-is. Click next for monitoring and choose the option to disable boot diagnostics. Press "next" and then "Review+create". Once the virtual machine is done validating, click create to complete the creation process of the virtual machine. 

<img width="1451" height="725" alt="Screenshot 2025-11-18 at 7 57 31 PM" src="https://github.com/user-attachments/assets/fc5c6641-0957-42cc-baf1-f845391a538e" />

Once the virtual machine is finished being created, you can go back into the resource group which will show you all of the components that goes with the virtual machine.

<img width="1450" height="725" alt="Screenshot 2025-11-18 at 7 59 14 PM" src="https://github.com/user-attachments/assets/b8d2ee5b-9eb0-41cb-90d8-0e8d3ee531bf" />

CONGRATULATIONS! We have created our virtual Machine. Using the public IP address of the virtual machine and the user log-in credentials we created, we can now open our virtual machine using RDP. The next step is to intentionally give access to the public internet. 
--

Giving Access to the Public Internet Steps
--

From the resource group page, click on our network security group. In this example from the picture above, the network security group is called "CORP-NET-EAST-1-nsg". Once you click on that, we will now disable the firewall by changing the inbound rules. 

<img width="1444" height="720" alt="Screenshot 2025-11-18 at 8 03 03 PM" src="https://github.com/user-attachments/assets/c725e10a-6185-405e-8543-a1b83467e263" />

Delete the inbound rule for RDP. We will then create a new rule that will allow any traffic from the public network to access the virtual machine. We will click on settings and then inbound security rules. There we will set up our rules and press add (this will allow all access to the virtual machine from the public internet):

<img width="1449" height="721" alt="Screenshot 2025-11-18 at 8 05 32 PM" src="https://github.com/user-attachments/assets/0a5368db-4d84-4647-88e5-8d5378d027de" />


<img width="1456" height="724" alt="Screenshot 2025-11-20 at 1 42 58 PM" src="https://github.com/user-attachments/assets/1d080853-4d61-4373-bbf7-13d41c0c0bfa" />

Once the new inbound rules are set the virtual machine is now open to being attacked from the public internet.

Creating the Log Repository Steps
--

We will begin by creating a log analytics workspace back in azure. Type "log analytics workspace" in the search box and then click on that option and press the create log analytics workspace button and you will come to a page that looks like this: 

<img width="1455" height="719" alt="Screenshot 2025-11-20 at 2 06 34 PM" src="https://github.com/user-attachments/assets/a5e84687-e270-4fd0-88f6-c326140219ed" />

Ensure to choose the resource group that we created from the drop down box and create a name and then hit review+create. This will create the log analytics repository. Once the log analytics workspace is finished being created, we can then create the Microsoft sentinel instance. 

In the search box, type "sentinel" and click on the Microsoft Sentinel option. Once there, click on the create Microsoft Sentinel button. We will then choose the log analytics workspace that we just created in order to add Microsoft Sentinel to that workspace. This will link our log analytics workspace to our Sentinel instance (SIEM). After that is completed we will then have to create a connection between our VM and the log repository within sentinel. 


Virtual Machine Connection to Log Repository Steps
--

Inside Sentinel, click the content management dropdown and then click the content hub option and in the search box type "Windows Security Event"

<img width="1443" height="718" alt="Screenshot 2025-11-20 at 2 26 14 PM" src="https://github.com/user-attachments/assets/5b80c0cc-a970-43a9-bc66-81688524df96" />

We will then click on Windows Security Event and press install. After installing we will then configure the security event. 

Once the security event is finished installing, under content hub, if we click on Windows Security Event we now have the option to manage. Click on the manage button. 

<img width="1431" height="710" alt="Screenshot 2025-11-20 at 2 31 19 PM" src="https://github.com/user-attachments/assets/2e0d893e-9181-4664-9952-daa1456c6d6c" />

Once you click manage, you will then check the box for Windows Security Events via AMA and press open connector page.

<img width="1440" height="709" alt="Screenshot 2025-11-20 at 2 35 20 PM" src="https://github.com/user-attachments/assets/df10c920-27b6-46a4-9a90-7cfd47fcac99" />


Once we are on the connector page, we are going to click on create data collection rule (this rule will allow the logs from our virtual machine to be forwared to our SIEM). We will create a name for the rule and ensure that we choose the resource group we created from the resource group drop down box.

<img width="1452" height="727" alt="Screenshot 2025-11-20 at 2 41 42 PM" src="https://github.com/user-attachments/assets/4004d3c1-6c52-4a23-a32f-bda8f5186653" />

We will then click next for resources where we will click on our virtual machhine. We then click next for collect.

<img width="1447" height="719" alt="Screenshot 2025-11-20 at 2 46 10 PM" src="https://github.com/user-attachments/assets/a2d4b08b-de86-4c86-a66f-dfea3cc344a4" />

We will  leave the collect page as-is. Then click next and create. Once everything is finished being created and installed the logs from our virtual machines will be sent to our repository and can be accessed by our siem.

<img width="1458" height="723" alt="Screenshot 2025-11-20 at 1 46 31 PM" src="https://github.com/user-attachments/assets/9217c2a3-4fbf-4f37-8265-cfa3273b1e7c" />

CONCLUSION
-

After being left open to the public internet for approx. 48hrs, there was a massive increase in attempts to gain access to the virtual machine. I have included the before and after attack maps below:

-Before

<img width="1448" height="723" alt="Screenshot 2025-11-19 at 1 26 00 AM" src="https://github.com/user-attachments/assets/13797859-9f39-4991-8903-795facac9f59" />

-After 48hrs

<img width="1453" height="726" alt="Screenshot 2025-11-20 at 1 40 43 PM" src="https://github.com/user-attachments/assets/048137e8-3138-4a1b-a4cf-c8a7215c3a6b" />


Upon completing this lab, I learned the importance of ensuring that our database is secured. Having the proper security rules set in place can make a huge difference in protecting our systems and the systems of the customer which in-turn can lower the risk of data breaches. 
