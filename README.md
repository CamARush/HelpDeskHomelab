# Creating my Active Directory & Microsoft 365 homelab

## Introduction

Here are the steps I took to create my Active Directory and Microsoft 365 homelab. I wanted to create this homelab to demonstrably showcase my skills in Active Directory and Microsoft 365 administration while practicing Autopilot deployments. 

---

## On-Premesis Active Directory Domain Controller

I installed Windows Server and accessed the server manager. 

<img width="829" height="624" alt="image" src="https://github.com/user-attachments/assets/ded00a91-4d97-4234-8cf5-cc0f6e10d8e2" />

Then installed Active Directory Domain Services.

<img width="824" height="617" alt="image" src="https://github.com/user-attachments/assets/614fd20b-9a20-49cf-9f63-9d131ac1b4da" />

Then configured the domain controller.

<img width="821" height="616" alt="image" src="https://github.com/user-attachments/assets/c5182f97-89a1-4973-8f1d-8f232554b0eb" />

Now I can Access Active Directory Users and Computers. 

<img width="822" height="616" alt="image" src="https://github.com/user-attachments/assets/eb779616-e873-4278-bd4d-a3b69aa4ca0d" />

<img width="824" height="619" alt="image" src="https://github.com/user-attachments/assets/52e899b5-80c6-48fe-87bd-05658a4660eb" />

I created their user account.

<img width="616" height="431" alt="image" src="https://github.com/user-attachments/assets/eaab51c1-199c-435c-8d0e-becfb78c3700" />

I created the IT Help Desk Security Group.

<img width="606" height="427" alt="image" src="https://github.com/user-attachments/assets/295dde99-12bd-4071-a58f-5646930c72f5" />

Now I can add them to that group. 

<img width="325" height="435" alt="image" src="https://github.com/user-attachments/assets/87815493-5203-4583-a48a-bed45c829ae2" />

I want to give all employees on the IT Help Desk team access to the documents folder on the domain controller. 

<img width="818" height="612" alt="image" src="https://github.com/user-attachments/assets/43212cfa-147e-4fed-8833-ae20e0a59046" />
<img width="490" height="360" alt="image" src="https://github.com/user-attachments/assets/b91a2b4b-5e79-40ec-95fd-e67825cf5612" />

To ensure that no other users have access to it, I have to set the permissions in advanced sharing options. 

<img width="286" height="362" alt="image" src="https://github.com/user-attachments/assets/5e15c969-da63-43e4-9123-b74f546f2bf1" />
<img width="290" height="360" alt="image" src="https://github.com/user-attachments/assets/6e2ee646-d004-4e35-870e-563605dc3b84" />

### Conclusion/Future Plans:
I just scratched the surface of what you can do with Active Directory. You can use security groups to apply the principle of least privilege to not just folders. You can use security groups for files, drives, folders, VPN access, Remote Desktop, Firewall rules, and Printers/Scanners. 

I plan to implement some of these ACs and also utilize Entra Connect to bridge the gap between On-Premesis AD and the Cloud for a hybrid-identity environment. While I believe most corporate environments have moved away from on-premesis AD domain controllers in favor of the cloud, some may be still in a hybrid identity environment or transferring to the cloud so this skill will be useful. 

---

## Microsoft 365 Administration and Autopilot Deployment

### Scenario: 
A new employee named 'Front Desk' has been hired to run the front desk, and I need to create an Autopilot deployement for their PC. 

### Prerequisite:
I need a Microsoft 365 Business Premium subscription, so I got a 30 day free trial. Now I can access the M365 Admin Center.
<img width="1428" height="731" alt="image" src="https://github.com/user-attachments/assets/ad308c55-fe99-43e3-98db-a9d0abe7edb4" />

### Steps:
### 1. Hardware Hash

First, I'm going to prep the PC for Autopilot. To do this, I need to get the Hardware Hash of the PC and upload it to Intune so I can utilize Autopilot.

I followed the documentation here: https://learn.microsoft.com/en-us/autopilot/add-devices

I decided to use the script below to upload the hash directly to Intune, as this avoids the initial Windows setup process. 

```
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
 Set-ExecutionPolicy -Scope Process -ExecutionPolicy RemoteSigned
 Install-Script -Name Get-WindowsAutopilotInfo -Force
 Get-WindowsAutopilotInfo -Online
```

<img width="782" height="501" alt="image" src="https://github.com/user-attachments/assets/24072f1e-8230-40a3-91c4-25fe5b06a646" />

<img width="764" height="499" alt="image" src="https://github.com/user-attachments/assets/5b8fc404-6929-4005-96c9-4305ee2778af" />

Once it's done syncing, the device should show up in the available devices for Autopilot. 

<img width="1095" height="441" alt="image" src="https://github.com/user-attachments/assets/ac18d925-ddf4-41ff-ad10-11f35cfad3ff" />


### 2. User Creation and License Assignment.

I'm going to create the user 'Front Desk' and assign it a M365 license.

<img width="1337" height="416" alt="image" src="https://github.com/user-attachments/assets/39be3889-5681-4f03-9f65-3f396bcb237d" />
<img width="984" height="671" alt="image" src="https://github.com/user-attachments/assets/46f2fbfa-2717-494f-be57-e84d75864f26" />


### 3. Group Creation and Assignment

Now I need to create a group where I'll be able to assign permissions and resources to. For this example I'll create the groups 'Windows 11 - Autopilot' and 'Front Desk'. I've decided to make 2 distinct groups, as there are some configuration profiles that I may want to apply for just Front Desk devices and not all devices using Autopilot. 

<img width="1141" height="635" alt="image" src="https://github.com/user-attachments/assets/59615e3b-c385-48a1-979a-b7ef0c5a7f1f" />

I also have to make sure that the User and Device is are assigned to these groups.

<img width="1419" height="457" alt="image" src="https://github.com/user-attachments/assets/81dc5580-ae1c-4e3a-9e77-4f99cb6e9a96" />
<img width="1421" height="452" alt="image" src="https://github.com/user-attachments/assets/152c6933-217b-4b98-af49-50c31af2fd41" />


### 4. Company Branding

I created a simple logo and added a simple greeting that shows when users first sign in. 

<img width="1114" height="644" alt="image" src="https://github.com/user-attachments/assets/16a3cd29-9b0c-4dfd-ab75-177e093d42df" />
<img width="718" height="273" alt="image" src="https://github.com/user-attachments/assets/6f63545d-25ec-4e2a-a27c-6714db7eba70" />
<img width="470" height="96" alt="image" src="https://github.com/user-attachments/assets/7b2e09c3-d924-4103-942f-0c12e0963d88" />


### 5. Autopilot Profile

Now I need to create an Autopilot profile corresponding with the type of PC I'm setting up. (Front Desk, IT, CEO, etc.) For this example i'll be setting up an account for a new front desk employee. 

<img width="820" height="581" alt="image" src="https://github.com/user-attachments/assets/cb2cdcbd-0316-4f2a-a0d2-5416a5816144" />
<img width="809" height="642" alt="image" src="https://github.com/user-attachments/assets/21ff82d7-b934-477a-b18b-1e8088e91e80" />
<img width="776" height="568" alt="image" src="https://github.com/user-attachments/assets/60c8c26a-c695-409c-87bb-d250a4ddc123" />
<img width="773" height="564" alt="image" src="https://github.com/user-attachments/assets/e327e912-8f5d-47d6-84a9-c016694fa2fe" />


### 6. Pre-Installed Programs

Now I'm going to specify which programs I want to be installed on the endpoint device by default. 

<img width="947" height="269" alt="image" src="https://github.com/user-attachments/assets/2ce3f173-973b-4b1e-b1ad-1bc86c084105" />

I'm chooing the Autopilot group so every joined device will have these apps. 

<img width="1174" height="683" alt="image" src="https://github.com/user-attachments/assets/049f2408-8b28-491f-babc-dd3de56d8820" />

I'm going to have autopilot install the Brave Browser, Company Portal, and Microsoft 365 Apps.

<img width="1372" height="635" alt="image" src="https://github.com/user-attachments/assets/d6e630de-c0b1-4445-b805-1e5dccc601c0" />


### 7. Program Restrictions

Now that the apps are installed, I want to create a configuration profile so Front Desk workers won't have access to apps like Device Manager. I'll asign this configuration profile to the Front Desk group.

<img width="1415" height="719" alt="image" src="https://github.com/user-attachments/assets/c5991f50-e702-4e14-9c24-9d1499f8a4c9" />
<img width="821" height="597" alt="image" src="https://github.com/user-attachments/assets/d1cf0e01-99e0-41a5-8c6c-45decfd2ff1f" />
<img width="1399" height="698" alt="image" src="https://github.com/user-attachments/assets/77bc574b-cdf1-4462-9b91-6f2524a9adf9" />


### 8. Autopilot Enrollment

Now that I'm done with all of the configurations, I'm going to assign the device to our Front Desk user. 

<img width="1415" height="489" alt="image" src="https://github.com/user-attachments/assets/5d1fdf23-8537-4fb4-8918-59f1dfc58725" />


### 9. Testing

I can see the logo I created and the welcome message.

<img width="729" height="490" alt="image" src="https://github.com/user-attachments/assets/15bcee58-011d-459b-9eaf-554c92f8942f" />

Here are the installed apps I configured to be installed by Autopilot

<img width="292" height="192" alt="image" src="https://github.com/user-attachments/assets/7bf8a5d0-b472-41f7-a661-1d02384eeabe" />

<img width="304" height="372" alt="image" src="https://github.com/user-attachments/assets/5429530b-2986-4b2a-84c4-87d1e22c7864" />

Here is the message I receive when attempting to open Device Manager.

<img width="480" height="221" alt="image" src="https://github.com/user-attachments/assets/1ba91385-44f3-436b-bfc1-661bd89025b8" />

I can also see the device in the Intune admin center.

<img width="1387" height="644" alt="image" src="https://github.com/user-attachments/assets/e899e60e-3049-4247-b4da-4af79be7bc84" />

## Technical Hurdles & Troubleshooting:
The most significant challenges I encountered during this project were Intune enrollment and a Sysprep execution failure. 

**__Intune Enrollment__**
<ul>

**Issue:** After successfully uploading the hardware hash via the ``` Get-WindowsAutopilotInfo -Online ``` script, the device began the OOBE process with the custom Autopilot branding I configured. However, the applications I designated for automatic installation in the Intune admin center weren't being installed.

**Investigation:** The device was successfully registered under Devices > Windows > Windows enrollment, however, I noticed that the Profile Status was set to "Not Assigned". I had created a Dynamic Device Group which I had configured to automatically enroll devices into autopilot. After confirming the group query was correct, I went to the internet to research this behavior and found that this could be a processing delay with Entra ID dynamic groups.

**Resolution:** I decided to add the device manually to the proper group to bypass the delay. The status in the Intune enrollment page changed to Assigned and after resetting the OOBE and signing in, the device was successfully enrolled in Intune and the apps I configured were automatically installed. 
</ul>

**__Sysprep Execution__**
<ul>

**Issue:** When attempting to run ``` sysprep.exe /generalize /oobe ``` it would return a generic error, preventing me from restarting the OOBE to test my Autopilot configuration.

**Investigation:** Rather than resetting the Windows image, I investigated the setupact.log located in ``` C:\Windows\System32\Sysprep\Panther ```. The error log identified that sysprep couldn't run on a drive with BitLocker encryption enabled. 

**Resolution:** I decided to decrypt the drive using ``` manage-bde -off C: ``` and monitoring the decryption status with ``` manage-bde -status ``` until it was fully decrypted. I was then able to run sysprep to restart the OOBE.

</ul>

## Future Plans:
I plan to make the most of my Microsoft 365 free trial and test different Microsoft 365 services like Purview and Defender and also try MDM. I also want to set up an endpoint device that connects to the local domain controller. Autopilot was my main priority, so that will be my next step. 

## Conclusion:
I have gained hands-on experience with endpoint management through Intune and cloud administration with EntraID. Additionally, by configuring RBAC, I was able to practice implementing the principle of least privilege. This homelab has prepared me to effectively manage and troubleshoot Microsoft 365 environments and Autopilot deployments in an enterprise settings. It also serves as a platform for me to continue to develop my Microsoft 365 skills by testing different Microsoft 365 services like Purview and Defender XDR. 
