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

CONGRATULATIONS! We have created our virtual Machine. The next step is to intentionally give access to the public internet. 
--

Giving Access to the Public Internet Steps
--

From the resource group page, click on our network security group. In this example from the picture above, the network security group is called "CORP-NET-EAST-1-nsg". Once you click on that, we will now disable the firewall by changing the inbound rules. 

<img width="1444" height="720" alt="Screenshot 2025-11-18 at 8 03 03 PM" src="https://github.com/user-attachments/assets/c725e10a-6185-405e-8543-a1b83467e263" />

Delete the inbound rule for RDP. We will then creat a new rule that will allow any traffic from the public network to access the virtual machine. We will click on settings and then inbound security rules. There we will set up our rules and press add (this will allow all access to the virtual machine from the public internet):

<img width="1449" height="721" alt="Screenshot 2025-11-18 at 8 05 32 PM" src="https://github.com/user-attachments/assets/0a5368db-4d84-4647-88e5-8d5378d027de" />
