# Creating my Active Directory & Microsoft 365 homelab

## Introduction

Here are the steps I took to create my Active Directory and Microsoft 365 homelab. I wanted to create this homelab to demonstrably showcase my skills in Active Directory and Microsoft 365 administration while practicing Autopilot deployments. 

---

## On-Premesis Active Directory Domain Controller

I installed Windows Server and accessed the server manager. 

<img width="829" height="624" alt="image" src="https://github.com/user-attachments/assets/cd1f605c-1a89-40e8-8d92-dd9b16721b63" />

Then installed Active Directory Domain Services.

<img width="824" height="617" alt="image" src="https://github.com/user-attachments/assets/469693f2-8346-4201-a148-d28b113ebe69" />

Then configured the domain controller.

<img width="821" height="616" alt="image" src="https://github.com/user-attachments/assets/d3a6d27a-d13d-40fa-9734-11dff518dc4b" />

Now I can Access Active Directory Users and Computers. 

<img width="822" height="616" alt="image" src="https://github.com/user-attachments/assets/7eb74477-2dc0-4be6-b904-7c68422f190d" />

<img width="824" height="619" alt="image" src="https://github.com/user-attachments/assets/1cbbdb2f-9c57-47e0-977f-8b29f4bbd9e0" />

I created their user account.

<img width="616" height="431" alt="image" src="https://github.com/user-attachments/assets/e38ed4e4-3325-446c-ac10-9110d96a64c1" />

I created the IT Help Desk Security Group.

<img width="606" height="427" alt="image" src="https://github.com/user-attachments/assets/fb94aeb7-8598-472f-9b98-e1d3495414fe" />

Now I can add them to that group. 

<img width="325" height="435" alt="image" src="https://github.com/user-attachments/assets/9e216657-0b5c-4e62-8489-fa4dc37002b4" />

I want to give all employees on the IT Help Desk team access to the documents folder on the domain controller. 

<img width="818" height="612" alt="image" src="https://github.com/user-attachments/assets/460f67db-6e71-4726-8149-94bb64c4b904" />
<img width="490" height="360" alt="image" src="https://github.com/user-attachments/assets/4a1bf77e-a4bd-4d70-b7e1-b94f2a4a010a" />

To ensure that no other users have access to it, I have to set the permissions in advanced sharing options. 

<img width="286" height="362" alt="image" src="https://github.com/user-attachments/assets/6e24e6a7-4226-4cc9-acee-ec4d551e17ef" />
<img width="290" height="360" alt="image" src="https://github.com/user-attachments/assets/3f0ff56e-0211-4d2e-9a2c-af1d46a66bf1" />

### Conclusion: 
While I believe most corporate environments have moved away from on-premesis AD domain controllers in favor of the cloud, some may be still in a hybrid identity environment or transferring to the cloud. 

I just scratched the surface of what you can do with Active Directory. You can use security groups to apply the principle of least privilege to not just folders. You can use security groups for files, drives, folders, VPN access, Remote Desktop, Firewall rules, and Printers/Scanners. 

---

## Microsoft 365 Administration and Autopilot Deployment

### Scenario: 
A new employee named 'Front Desk' has been hired to run the front desk, and I need to create an Autopilot deployement for their PC. 

### Prerequisite:
I need a Microsoft 365 Business Premium subscription, so I got a 30 day free trial. Now I can access the M365 Admin Center.
<img width="1428" height="731" alt="image" src="https://github.com/user-attachments/assets/d656cbee-5188-4f5d-8a15-81e93470907f" />

### Steps:
### 1. Hardware Hash

First, I'm going to prep the PC for Autopilot. To do this, I need to get the Hardware Hash of the PC and upload it to Intune so I can utilize Autopilot.

I followed the documentation here: https://learn.microsoft.com/en-us/autopilot/add-devices

I decided to use a script to upload the hash directly to Intune, as this avoids the initial Windows setup process. 

<img width="782" height="501" alt="image" src="https://github.com/user-attachments/assets/6ee442bb-b27e-49fd-b05d-a3c3519ff5df" />

<img width="764" height="499" alt="image" src="https://github.com/user-attachments/assets/5def9a8d-5cee-452f-b3c1-00b631f3f89b" />

Once it's done syncing, the device should show up in the available devices for Autopilot. 

<img width="1095" height="441" alt="image" src="https://github.com/user-attachments/assets/02d89b3c-2490-40d6-8e09-8e312c17d31c" />


### 2. User Creation and License Assignment.

I'm going to create the user 'Front Desk' and assign it a M365 license.

<img width="1337" height="416" alt="image" src="https://github.com/user-attachments/assets/feed5da9-5a62-43b0-8a87-e6f9899bab28" />
<img width="984" height="671" alt="image" src="https://github.com/user-attachments/assets/bcf3fe53-e088-4ecf-b667-827d7f3ee59a" />


### 3. Group Creation and Assignment

Now I need to create a group where I'll be able to assign permissions and resources to. For this example I'll create the groups 'Windows 11 - Autopilot' and 'Front Desk'. I've decided to make 2 distinct groups, as there are some configuration profiles that I may want to apply for just Front Desk devices and not all devices using Autopilot. 

<img width="1141" height="635" alt="image" src="https://github.com/user-attachments/assets/013c3fd5-9da8-46cb-9a2a-06f21ea091c8" />

I also have to make sure that the User and Device is are assigned to these groups.

<img width="1419" height="457" alt="image" src="https://github.com/user-attachments/assets/ebc07fbd-7dc3-46ed-a33a-916c123e353a" />
<img width="1421" height="452" alt="image" src="https://github.com/user-attachments/assets/e2cfb1fb-e319-4d52-a634-12928b5346e9" />


### 4. Company Branding

I created a simple logo and added a simple greeting that shows when users first sign in. 

<img width="1114" height="644" alt="image" src="https://github.com/user-attachments/assets/eb90f60a-4271-4005-88e7-8cc739395344" />
<img width="718" height="273" alt="image" src="https://github.com/user-attachments/assets/79c383de-3722-4fe8-a7e6-5057f21cf752" />
<img width="470" height="96" alt="image" src="https://github.com/user-attachments/assets/224dca8e-80ef-49b5-ae90-dc0292f29f2f" />


### 5. Autopilot Profile

Now I need to create an Autopilot profile corresponding with the type of PC I'm setting up. (Front Desk, IT, CEO, etc.) For this example i'll be setting up an account for a new front desk employee. 

<img width="820" height="581" alt="image" src="https://github.com/user-attachments/assets/87a879c7-14c8-426a-8bf2-b7bbbc5614aa" />
<img width="809" height="642" alt="image" src="https://github.com/user-attachments/assets/d090bf63-d9a2-4514-949d-f9786a5641ab" />
<img width="776" height="568" alt="image" src="https://github.com/user-attachments/assets/51f287fb-6b9c-452a-a683-95056083afef" />
<img width="773" height="564" alt="image" src="https://github.com/user-attachments/assets/e961d59c-5173-4017-9d02-8e2a7b313de7" />


### 6. Pre-Installed Programs

Now I want to add specific programs that will be installed by default. For this example I want all M365 apps to be installed and 

<img width="947" height="269" alt="image" src="https://github.com/user-attachments/assets/5883d27f-1d7d-459a-ab6a-fe1a0dccd238" />

I'm chooing the Autopilot group so every joined device will have these apps. 

<img width="1174" height="683" alt="image" src="https://github.com/user-attachments/assets/cf85ff4c-5ffd-4696-9ce5-115f22d44a7d" />

I'm going to have autopilot install Brave Browser, Company Portal, and Microsoft 365 Apps.

<img width="1372" height="635" alt="image" src="https://github.com/user-attachments/assets/6a39c569-77c0-4a60-8da6-ab25907cc2cb" />


### 7. Program Restrictions

Now that the apps are installed, I want to create a configuration profile so Front Desk workers won't have access to apps like Device Manager. I'll asign this configuration profile to the Front Desk group.

<img width="1415" height="719" alt="image" src="https://github.com/user-attachments/assets/69f8f182-ec1d-4ab0-a304-1056b0972e76" />

<img width="821" height="597" alt="image" src="https://github.com/user-attachments/assets/468ebd09-9e21-402c-8f71-8bc7e52bad61" />

<img width="1399" height="698" alt="image" src="https://github.com/user-attachments/assets/349f3a80-591c-4a12-acb9-24066a2f0546" />


### 8. Autopilot Enrollment

Now that I'm done with all of the configurations, I'm going to assign the device to our Front Desk user. 

<img width="1415" height="489" alt="image" src="https://github.com/user-attachments/assets/1d875eee-074b-4b4f-b3f6-94b3f9ab8a27" />


### 9. Testing

I can see the logo I created and the welcome message.

<img width="729" height="490" alt="image" src="https://github.com/user-attachments/assets/b10ac21f-c696-4343-9d0c-2508a1baa17c" />

Here are the installed apps I configured to be installed by Autopilot

<img width="292" height="192" alt="image" src="https://github.com/user-attachments/assets/6461047a-17f4-4fcf-b070-6f248ecfe724" />

<img width="304" height="372" alt="image" src="https://github.com/user-attachments/assets/b09c6458-1af7-4444-94b0-7ce68b3dd2eb" />

Here is the message I receive when attempting to open Device Manager.

<img width="480" height="221" alt="image" src="https://github.com/user-attachments/assets/14632506-40a9-4dd5-8b3b-6525334ec6cd" />

I can also see the device in the Intune admin center.

<img width="1387" height="644" alt="image" src="https://github.com/user-attachments/assets/98f57395-121c-44e9-9215-20f9e5b75b1d" />


## Future Plans:
I plan to make the most of my Microsoft 365 free trial and test different Microsoft 365 services like Purview and Defender. I also want to set up an endpoint device that connects to the local domain controller. Autopilot was my main priority, so that will be my next step. 

## Conclusion:
I learned a lot about Autopilot and how to customize the OOBE. Specifically by enrolling a device in Entra ID and Intune to have a zero-touch autopilot setup. I also honed my skills in policy and group configuration.
