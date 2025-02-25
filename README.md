# Azure-SIEM-Lab

## Objective

The Azure SIEM Lab project aimed to establish a controlled environment in Azure for simulating and detecting cyber attacks. The primary focus was to ingest and analyze logs within Microsoft Sentinel, a Security Information and Event Management (SIEM) system, generating telemetry to locate and map real-world attacks. This hands-on experience was designed to deepen understanding of network security, attack patterns, and defensive strategies.

### Skills Learned

- Used custom PowerShell script to extract metadata from Windows Event Viewer to be forwarded to third party API in order to derive geolocation data
- Configured Log Analytics Workspace in Azure to ingest custom logs containing geogrphic information
- Configured Microsoft Sentinel workbook to display global attack data (RDP brute force) on world map

### Tools Used

- Azure
- PowerShell
- Log Analytics Workspace
- Microsoft Sentinel (cloud SIEM)

## Steps


#### Step 1:
- [Create Free Azure Subscription](https://azure.microsoft.com/en-us/pricing/purchase-options/azure-account)

#### Step 2:
- Once created, login at https://portal.azure.com

#### Step 3:
- Open ‘Resource groups’, then click ‘Create’

![Step 3](https://github.com/user-attachments/assets/30f9aa04-c2cb-450f-9b3c-7c4772c8768a)

#### Step 4:
- Name the resource group *(e.g. RG-SOC-Lab)* and select a region *(e.g. East US 2)*

![Step 4](https://github.com/user-attachments/assets/06d368f9-cfb8-4c5f-8491-47ba256e13f7)

#### Step 5:
- Click ‘Review + Create’, then click ‘Create’

#### Step 6:
- Using the search bar, enter ‘virtual networks’, then click ‘Create’

![Step 6](https://github.com/user-attachments/assets/b7320195-bc0b-4fa6-a7a0-bbdfcf35b975)

#### Step 7:
- Select the resource group, give the network a name *(e.g. Vnet-SOC-Lab)*, and confirm the region

![Step 7](https://github.com/user-attachments/assets/57e2c512-b4a7-4473-a31e-a63d311df5b1)

#### Step 8:
- Click ‘Review + Create’, then click ‘Create’

#### Step 9:
- Using the search bar, enter ‘virtual machines’, then click ‘Create’

![Step 9](https://github.com/user-attachments/assets/0dc1c0f7-2953-4f20-91bd-fbadc255db57)

#### Step 10:
- Select the resource group, give the machine an innocuous name *(e.g. CORP-NET-EAST-1)*, and confirm the region

*(Reason for the name is so it’s not TOO obvious of a honeypot)*

![Step 10](https://github.com/user-attachments/assets/08e84481-12ff-4885-b992-c99d824307d6)

#### Step 11:
**IMPORTANT:** 
- The below settings speed up the lab.
- The image and size shown can only be used in Zone 2/3.
- Free accounts have $200 in credit, so no card charges will be made.

![Step 11](https://github.com/user-attachments/assets/adc1800d-4300-4131-a81f-7e9a2e6c45b6)

#### Step 12:
- Username: labuser
- Password: Cyberlab123!
- Check the Licensing Agreement, then click 'Next'

![Step 12](https://github.com/user-attachments/assets/f098bcd6-53d9-45ae-b084-9184badefa2f)

#### Step 13:
- Select 'Premium SSD', then click 'Next'

![Step 13](https://github.com/user-attachments/assets/7ed71bcb-7acb-49f2-a03f-f60f3d84aa3b)

#### Step 14:
- Select your created network, confirm Subnet is default and Public IP name

![Step 14](https://github.com/user-attachments/assets/f5ae5b87-0dde-4bbc-a2a6-6df32f01be6a)

#### Step 15:
- Scroll down and select 'Delete Public IP and NIC when VM is deleted'

![Step 15](https://github.com/user-attachments/assets/b6ef7544-7857-4d26-9170-feec606b661b)

#### Step 16:
- Click 'Next' until 'Monitoring', then disable 'Boot diagnostics'

![Step 16](https://github.com/user-attachments/assets/9f51484f-5a47-402a-ac07-e20d3456e2a2)

#### Step 17:
- Click ‘Review + Create’, wait for validation, then click ‘Create’

#### Step 18:
- Once deployment is complete, using the search bar, enter ‘Resource groups’ 

#### Step 19:
- In your resource group, open the item ending in '-nsg'

![Step 19](https://github.com/user-attachments/assets/63f788f0-320e-498d-8ff9-5184901a3916)

#### Step 20:
- Delete the RDP

![Step 20](https://github.com/user-attachments/assets/68c27c4c-7c6b-4372-a3a1-d61f3b65fb26)

#### Step 21:
- On the left side-bar, click 'Settings', then 'Inbound security rules'

![Step 21](https://github.com/user-attachments/assets/2a5ebb6d-7c52-4fa9-9dbb-9cd3d9dc608f)

#### Step 22:
- Change the destination port ranges to * , then click 'Add'

![Step 22](https://github.com/user-attachments/assets/f1608c5b-5e24-4079-a73f-5319414c593c)

#### Step 23:
- Using the search bar, enter ‘virtual machines’, then click on your virtual machine

#### Step 24:
- Find and copy the Public IP address

![Step 24](https://github.com/user-attachments/assets/34b3c100-02dc-44a8-81af-72215d3cc449)

#### Step 25:
- Hit the Windows Start button, type 'mst' then hit Enter

#### Step 26:
- Paste the Public IP into 'Computer', then click 'Connect'

![Step 26](https://github.com/user-attachments/assets/f906b2e9-04ca-4811-84c9-a5c8ddef1531)

#### Step 27:
- In the VM, hit the Windows Start button, type 'wf.msc' then hit Enter

#### Step 28:
- Click 'Windows Defender Firewall Properties'

![Step 28](https://github.com/user-attachments/assets/59b418e6-ba73-4a9f-9216-a31a7faab154)

#### Step 29:
- Turn off everything in 'Domain Profile', 'Private Profile, and 'Public Profile'

![Step 29](https://github.com/user-attachments/assets/4caf4c47-0097-431a-9975-c6f40f94d241)

#### Step 30:
- On your PC, open Powershell and type:

```
ping [public ip address]
```

![Step 30](https://github.com/user-attachments/assets/22089669-3188-47c8-a01b-79d651ebae72)

#### Step 31:
- Using the search bar, enter ‘log analytics workspaces’, then click ‘Create’

![Step 31](https://github.com/user-attachments/assets/06cc2e20-5c9f-47f4-953a-59c3c520350b)

#### Step 32:
- Select the resource group, give it a name *(e.g. LAW-soc-lab-0000)*, and confirm the region

![Step 32](https://github.com/user-attachments/assets/65cb5ae6-264e-4723-9cc5-a9a9b6684ac9)

#### Step 33:
- Click ‘Review + Create’, then click ‘Create’

#### Step 34:
- Using the search bar, enter ‘microsoft sentinel’, then open your LAW

![Step 34](https://github.com/user-attachments/assets/4d934978-a13f-46bd-9e3d-f3a848783022)

#### Step 35:
- On the left side-bar, click 'Content management', then 'Content hub'

![Step 35](https://github.com/user-attachments/assets/525264d0-3843-4436-8407-d54a2f2077ef)

#### Step 36:
- Using the search bar, type 'security event', then select 'Windows Security Events' and click 'Install'

![Step 36](https://github.com/user-attachments/assets/4ea75209-928f-4859-91e4-55ce7c427cc0)

#### Step 37:
- Once installed, click 'Manage'

![Step 37](https://github.com/user-attachments/assets/a8a37644-0243-4302-8e3b-22a4f30491bf)

#### Step 38:
- In a seperate tab, open Microsoft Azure and navigate to 'Virtual machines'

#### Step 39:
- Click on your VM, click 'Settings', then click 'Extensions + applications'

![Step 39](https://github.com/user-attachments/assets/f9746790-4b99-4a51-aec1-7e1820b9e010)

#### Step 40:
- Back in the security events tab, select 'Windows Security Events via AMA', then click 'Open connector page'

![Step 40](https://github.com/user-attachments/assets/525e09dc-c0ea-407f-8db5-1b1668576891)

#### Step 41:
- Click 'Create data collection rule'

![Step 41](https://github.com/user-attachments/assets/82d02e79-40f4-4f85-8f81-14b2cb3ef479)

#### Step 42:
- Give a rule name *(DCR-Windows)*, confirm resource group, then click 'Next'

![Step 42](https://github.com/user-attachments/assets/5f505f94-e67b-4982-ae90-c2e7b1d9a6ac)

#### Step 43:
- Expand and select each option in the 'Resources' tab

#### Step 44:
- Click ‘Review + Create’, then click ‘Create’

![Step 44](https://github.com/user-attachments/assets/a0770f26-a158-4124-bbf0-79bbbf26f5c8)

#### Step 45:
- Go back to the 'Extensions + applications' tab and refresh until you see 'Provisioning succeeded'

![Step 45](https://github.com/user-attachments/assets/d9e0ea5b-27ac-4fc1-a8b9-2dfdf7872da7)

#### Step 46:
- In a seperate tab, open Microsoft Azure and navigate to 'Log Analytics workspaces'

#### Step 47:
- Open your LAW then select 'Logs'

#### Step 48:
- Take a break for 20-30mins to wait for activity

#### Step 49:
- Type 'SecurityEvent' then click 'Run'

![Step 49](https://github.com/user-attachments/assets/e250862b-4ef6-4d6b-95d4-a70c678416bb)

#### Step 50:
Find an account name and use the following command:

```
SecurityEvent
| where Account == "\\<insertname>"
```

![Step 50](https://github.com/user-attachments/assets/d1d2cea2-0037-41cb-9bef-4797bb5d2a25)

#### Step 51:
We can even view specific info using the following command:

```
SecurityEvent
| where Account == "\\<insertname>"
| project TimeGenerated, Account, Computer, EventID, Activity, IpAddress
```

![Step 51](https://github.com/user-attachments/assets/11ba21d2-5be3-4313-96e5-2b1c3ca1820c)

#### Step 52:
We can also view failed logins with the following command:

```
SecurityEvent
| where EventID == 4625
| project TimeGenerated, Account, Computer, EventID, Activity, IpAddress
```

![Step 52](https://github.com/user-attachments/assets/32d3728b-b64c-418d-97be-d4317a267daa)

#### Step 53:
There is no location data, only IP addresses, which we can use to derive the location data. We do this by importing a spreadsheet (as a 'Sentinel Watchlist') which contains geographic information for each block of IP addresses.

[Download Here](https://drive.google.com/file/d/13EfjM_4BohrmaxqXZLB5VUBIz2sv9Siz/view)

#### Step 54:
- In a seperate tab, open Microsoft Azure and navigate to 'Microsoft Sentinel'

#### Step 55:
- Open your LAW, click 'Configuration', then 'Watchlist', then click 'New'

![Step 55](https://github.com/user-attachments/assets/ae724e32-b576-4044-8e02-7b3fe9ee3ca5)

#### Step 56:
- Name/Alias: geoip
- Source type: Local File
- Number of lines before row: 0
- Search Key: network

#### Step 57:
- Refresh unti finished uploading

![Step 57](https://github.com/user-attachments/assets/4279af00-fcc0-476e-be67-f3f2da593a80)

#### Step 58:
- Once finished, go back to the LAW logs tab and run the following:

```
let GeoIPDB_FULL = _GetWatchlist("geoip");
let WindowsEvents = SecurityEvent
    | where IpAddress == <attacker IP address>
    | where EventID == 4625
    | order by TimeGenerated desc
    | evaluate ipv4_lookup(GeoIPDB_FULL, IpAddress, network);
WindowsEvents
| project TimeGenerated, Computer, IpAddress, cityname, countryname, latitude, longitude
```

![Step 58](https://github.com/user-attachments/assets/d1bd256c-3179-4a46-a55d-9423cc83cafb)

*(Observe the architecture)*

#### Step 59:
- Once command is run, go back to the Microsoft Sentinel tab, click 'Threat Management', then 'Workbooks', then click 'Add Workbook'

![Step 59](https://github.com/user-attachments/assets/4259c1c7-655f-4937-8e9c-3ae05e690b86)

#### Step 60:
- Select edit then remove all pre-made elements

#### Step 61:
- [Copy this!](https://drive.google.com/file/d/1ErlVEK5cQjpGyOcu4T02xYy7F31dWuir/view)

#### Step 62:
- Click 'Add', then 'Add query'

#### Step 63:
- Select 'Advanced Editor', paste the text, then click 'Done Editing'

![Step 63](https://github.com/user-attachments/assets/4e80b3f8-a902-4669-b31d-7109691be435)

#### Step 64:
You now have a VM Attack Map

![Step 64](https://github.com/user-attachments/assets/001346f6-4d64-42d6-9c87-092d4dd30f8f)

#### Step 65:
- Save the map within your resource group

![Step 65](https://github.com/user-attachments/assets/e1139149-3d7b-4b65-85ad-5f7a114663b7)

#

**IMPORTANT:**
In order to prevent any future charges for Azure services, make sure to fully shutdown and deallocate your virtual machine after finishing this lab if you have no further use for this specific machine.
