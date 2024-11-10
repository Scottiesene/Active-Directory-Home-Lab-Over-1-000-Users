![image](https://github.com/user-attachments/assets/4db8495b-231d-405a-9bae-b7c0fa76e70f)


## Introduction
This project was created to show knowledge of Active Directory concepts. Powershell is also utilized to create over 1,000 users in the home lab to simulate an enterprise environment to practice creating roles and access controls.
## Giving IP addressing to our newly downloaded SERVER 2016 Instance
![image](https://github.com/user-attachments/assets/8c2f12fb-5eec-4053-8911-714b201c27e3)

![image](https://github.com/user-attachments/assets/131cb61c-2a20-4976-9eb0-fe1d4f2e825d)

It is important that we configure what will be our domain controller under NAT. This is essentially the creation of two Network interface cards. The first, pictured above is going to be getting its addressing from the home router. The second, displayed below is being created to simulate an internal network interface card that could be used in an enterprise environment where one Active Directory Domain is configured to allow users from another Active Directory Domain access. This is a "trust" in a nutshell. This can be seen in the initial diagram for the project where they are connected via the virtual network. Although I will be focusing on the creation of the Active Directory domain only for Company A in this project, this is still a good example for an idea of how it could work in the real-world.
![image](https://github.com/user-attachments/assets/cd6ed597-0d0f-4d07-a150-705ca7f2f4d2)

Displayed below is the demonstration of the external NIC getting its addressing from the home router.
![image](https://github.com/user-attachments/assets/1b474f70-888a-409b-8691-cc297e0de712)

In this step we are giving the internal NIC an IP. There is no gateway because the domain controller itself is going to serve as the gateway. The loopback is used so that the computer will use itself at the DNS.
![image](https://github.com/user-attachments/assets/f2cc90d4-2281-4b33-ae2b-2dff7de1f325)

It is also important to rename them to avoid confusion
![image](https://github.com/user-attachments/assets/d59d0147-ee88-4fea-8b8e-e85e4e597b7d)


## Installing Active Directory

Once this is complete, we will begin the installation of Active Directory and create the domain.
![image](https://github.com/user-attachments/assets/fb8c6264-738a-43a5-b266-cb8f1ed20809)

![image](https://github.com/user-attachments/assets/b85e405d-acf8-47fb-969b-418300f01b68)

Be sure to enable group policy management as pictured below.

![image](https://github.com/user-attachments/assets/c50fd809-1627-448d-9107-4443629498b6)

![image](https://github.com/user-attachments/assets/c4a5b3a8-8698-422f-883e-1d2f2a32aa6e)

Once the role has been installed, the post deployment configuration setting must be addressed.

![image](https://github.com/user-attachments/assets/973fa44d-a55b-44ac-b192-bcfd3dd22a4e)

At this point the software for Active Directory Domain Services (AD DS) but the domain itself is yet to be created. In order to promote this computer to a domain. The option for create a new forest must be selected. For my project, I will be naming the domain something simple; "mydomain.com".

![image](https://github.com/user-attachments/assets/a28ab06a-28e7-47e2-8e3a-aa12bda9d042)
![image](https://github.com/user-attachments/assets/4a075515-ee1f-4537-a52b-14ab6e8c4284)

Once finished, the computer will restart.

![image](https://github.com/user-attachments/assets/2c67e4d9-da1d-4e4e-a236-0a5f96e6ab52)

You will notice that the username will change from just the username, to MYDOMAIN/username once loaded back in.

![image](https://github.com/user-attachments/assets/ede0f3f1-fb52-4cf9-bbfa-6bc28d3f99a1)


## Creating our own Dedicated Domain Admin Account

Creating our own dedicated domain admin account rather than just using the built in admin account, can be done by navigating to the Active Directory Users and Computers options.

![image](https://github.com/user-attachments/assets/c6eaa108-4fd4-462e-affd-b9026e904114)

Once inside, an organizational unit (OU) will be created to put our admin account in. The OU in this example is essentially playing the part of a folder in AD, and it will be named _ADMINS.
![image](https://github.com/user-attachments/assets/16a13e90-6011-47f7-858f-96724975643f)
![image](https://github.com/user-attachments/assets/10c162ef-0f1a-4dc7-b05a-26e74739d92e)

After navigating to that newly created folder, we will create a new user.
![image](https://github.com/user-attachments/assets/ab2f1055-d474-4105-82d4-b70b5093b59a)

In this case I am using myself as an example. For the username, I will be following a common naming convention used in organizations (First Inital Last Name). The "a-"before the name signifies that this account is an admin account.
![image](https://github.com/user-attachments/assets/9704baa9-d57f-4207-a368-e46387d510cc)
![image](https://github.com/user-attachments/assets/bc12fa52-fb09-481f-91eb-4baa3d863e43)

Even though we used the "a-", we are still not labeled as an Admin. We have to go Properties, Navigate to the "Member Of" tab, and ourselves to Domain Admins. 

![image](https://github.com/user-attachments/assets/eac95081-a57a-4697-8004-5edd16fd8dc0)


![image](https://github.com/user-attachments/assets/ff215574-45b5-4ad3-bae0-5a720fe8e5c1)


![image](https://github.com/user-attachments/assets/8592e21d-6686-4dc0-ac5d-81156b4f94ea)

![image](https://github.com/user-attachments/assets/10dc0146-9d2c-4062-bc7b-f640d2f96450)

![image](https://github.com/user-attachments/assets/8b4a4337-5945-4cf4-b3dd-d3a6cc709d5f)

After this step, we have our very own domain admin account. To use this we will need to sign out, and log back in as our dedicated admin.

![image](https://github.com/user-attachments/assets/0a7467e4-e5bf-4386-8104-9aea6c378293)

Pictured above, the account information has been pulled from Active Directory and we have been logged in.

## Installing Remote Access Server / Network Address Translation


The next step is to install RAS / NAT. This is an important step because we are simulating an enterprise enviornment. In this example, the RAS / NAT installation would allow a client (Simulated Company B) to be on the private virtual network, but still access the internet through the domain controller.

![image](https://github.com/user-attachments/assets/b1556300-ab23-41f5-8d81-44b329fb7a89)

![image](https://github.com/user-attachments/assets/ab0be96a-ce88-4c81-a1cc-5a612948013e)

![image](https://github.com/user-attachments/assets/44005c17-875b-4de5-9e8a-ea4c58a1ff79)

After the install is complete, navigate to Routing and Remote Access under Tools.

![image](https://github.com/user-attachments/assets/28ef41de-fd82-478e-8160-cefd2e10a456)

![image](https://github.com/user-attachments/assets/c46359a4-efcf-4a56-911c-8d297fbe1778)

Once in the configuration settings, NAT needs to be enabled to allow internal clients to connect to the internet using one public IP address.

![image](https://github.com/user-attachments/assets/5e3604fe-9019-4ccc-9374-85362ce4707c)

Be sure to select the public interface because it will be used to connect to the internet. In my case it is named "INTERNET". Once this is complete there should be a green arrow to indicate it is up and running. 

![image](https://github.com/user-attachments/assets/3812ffe0-1ed2-41d5-a3aa-2bcbd4ff6e64)

## Setting up the DHCP

This step is another that is very important for simulation purposes. So far we have created the Domain Controller and configured Active Directory Domain Services, as well as RAS/NAT. If there were to be clients they would need a DHCP Server to get IP addressing from the Domain Controller. This will allow those clients to get on the internet and browse the internet even though they will be connected through what would be our virtual private network. This is similar to how offices and schools operate as well.

![image](https://github.com/user-attachments/assets/4e07df80-aa41-4a07-a5dd-3bc4ffc9d522)

![image](https://github.com/user-attachments/assets/4ad79be7-8fe7-4bc0-b08c-87cbb48a7819)

After installation navigate to DCHP Control Panel

![image](https://github.com/user-attachments/assets/68e486c0-55df-4eb5-a11f-ea74992532a6)

Now the scope needs to be configured.

![image](https://github.com/user-attachments/assets/7e23b9cc-9cc6-4c6d-81c8-07827b1d548a)

![image](https://github.com/user-attachments/assets/13a60434-ed42-47c2-b625-fb6eb3912afe)

Here I am just naming the scope after the IP Range.

![image](https://github.com/user-attachments/assets/33aaba30-cb0b-4edc-86b3-b4b22bbead35)

![image](https://github.com/user-attachments/assets/f23e9dec-8402-464b-b182-80824e61db0b)

Lease duration is being left default for the lab, however in an enterprise environment there would be time limits like 8 hours for the workday, for example. Imagine if Starbucks kept the lease duration for 8 days. If someone connected to the network for an hour they would still have that lease. If many people are coming to that location over that period of time, they could run into issues with connectivity.

![image](https://github.com/user-attachments/assets/9fc26877-1c87-4f8e-939d-4217fce67c4f)

Configure the default gateway and Activate Scope. In this case the internal NIC of the domain controller is serving as the gateway.

![image](https://github.com/user-attachments/assets/aa67c616-2313-48f2-8f64-5c648ff8547c)

![image](https://github.com/user-attachments/assets/47a42393-4f2a-4932-83d5-acd71d61ea36)

Once completed the server should be up and running.

![image](https://github.com/user-attachments/assets/470772e4-d12a-4a64-ace1-6dcc2cd1d5ee)

The DHCP server is now COMPLETE!

## Creating users using POWERSHELL!!

The creation of users here will be crucial in speeding up the process to generate a large number of accounts to aid in simulating the enterprise enviornment we are aiming to create. In my example I will be utilizing some sample code and explaining each line of said code to display some knowledge and understanding. After finishing the project, I will also go into an account to comment on some actions that can be taken. 

Here I am opening Powershell as an admin and opening the sample script.

![image](https://github.com/user-attachments/assets/be57c9b3-4f2c-43cd-bfdc-6be70c02c79b)

![image](https://github.com/user-attachments/assets/350919bd-0ff6-4f48-a47d-affdd544c421)

To avoid errors input “Set-ExecutionPolicy Unrestricted” as I have below.

![image](https://github.com/user-attachments/assets/e26519d8-faa9-4eb9-bea4-50c3dae47be4)

Before running the script I will explain the function of each line.

## PowerShell Script Explanation

![image](https://github.com/user-attachments/assets/cc6f8bad-f6ac-47db-b589-d68a128c0daf)


1.	Comment for Variables
2.	Password that all user accounts will use. In this case “Password1”
3.	Get-Content from .\names.txt essentially takes all of the names from the document and puts them into $USER_FIRST_LAST_LIST essentially as an array.
4.	X
5.	X
6.	This line of code takes the plaintext password, in this case “password1” and turns it into an object Powershell can use as a secure password. This is used later on in line 15, when we are creating the users in Active Directory.
7.	Essentially all this line does is create an organizational object titles_USERS rather than _ADMIN
8.	X
9.	The $USER_FIRST_LAST_LIST contains a list of all the users and lines 9-24 will run for each of those users. For example, the first “$n” will be Scottie Senephimmachac.
10.	The “$n” is split. In this case Scottie Senephimmachac is split by the space between the names, the element Scottie is placed in the “$first” variable. Displayed in lowercase
11.	The “$n” is split. In this case Scottie Senephimmachac is split by the space between the names, the element Senephimmachac is placed in the “$last” variable. Displayed in lowercase
12.	The variable $username is created by taking the first character of the first name and glue it to the last name. Displayed in lowercase. Therefore, Scottie Senephimmachac becomes ssenephimmachac.
13.	Alerts that a user is being created in the color cyan.
14.	X
15.	Creates a new user in Active Directory.
16.	Passes in the first name from Line 10.
17.	Passes in the last name from Line 11
18.	Display Name is passed in from Line 12
19.	Name is passed in from Line 12
20.	Employee is passed in from Line 12
21.	Equivalent to checking the box for the option for the password not to expire when creating users manually.
22.	Puts the user into the organizational unit _USERS that will be created in Line 7.
23.	Just means that the user account will be enabled.
24.	X

When this code is ran the 1,000 names in the names.txt file will be pulled and create all of the users.

Below we see the result of line 13. This is why there is the black background and cyan text.

![image](https://github.com/user-attachments/assets/e10e631e-e179-46bd-957b-3d8db3973cee)


## RESULTS

After the script has finished running, we can navigate back to our Active Directory. Inside we will see that the _Users folder (OU) has been created and there are many users inside.

![image](https://github.com/user-attachments/assets/aebe702b-9eb1-4bd7-bd6a-2157e958184d)


Before running the script I made sure to edit the names.txt file and input my name. Due to this I am able to go to the domain and search for myself.

![image](https://github.com/user-attachments/assets/e5e40b61-e123-4ad1-854f-ba1975089fed)

AT THIS POINT WE ARE FINISHED!! You will notice from the original network diagram below, that we have completed the scope of our project, and the only thing we havent created is that second company. This second company is meant to be simulated, which is why we went through the steps to create what would be needed for them to access that internal network, had this been a real world scenario involving trusts and/or clients.

![image](https://github.com/user-attachments/assets/a447bee4-21fb-4359-a0a4-c92388f65b69)


## Some user account options

After selecting a random account, I am going in to look at some of the properties such as the first name last name and username.

![image](https://github.com/user-attachments/assets/071a7142-1fec-45ca-85f0-2533b5b1a290)

Looking a bit more we can find options to change, add, or delete the user from different groups.

![image](https://github.com/user-attachments/assets/46c577c4-b6f6-4e9b-86a3-82ed59833b37)

The organization tab here could be especially useful for large organizations that use trusts. This is because the information that would beprovided here could help with ensuring users are assigned to the correct groups and roles, as well as help determine the resources that user should have access to.

![image](https://github.com/user-attachments/assets/65a71d6d-5634-4bd5-827b-5f0054c9b1d6)


## CONCLUSION / SUMMARY

This project was conducted with the goal of demonstrating an understanding of Active Directory, trusts, and the importance of users having the correct permissions and access. 
First, I created a Domain Controller with 2 NICs. One for accessing the Internet and the other to simulate what would be an internal network. 
Second, I created  and configured the RAS / NAT for the purpose of allowing the simulated clients to be on the private virtual network, while still being able to access the internet through the domain contoller. Installing Remote Access Server / Network Address Translation on the domain controller makes this possible.
After the completion of the RAS / NAT installation, I created a DHCP Server. This would allow the simulated clients to automatically recieve IP addresses on the internal network.
Next was the use of Powershell to create the Users to help simulate our own enterprise environment. The script created 1000 users with a first initial last name naming convention similar to many organizations.
Now that the users are created, I am able to go into my virtualbox and tinker with the users access and roles. At this point the scope of the project has been completed with the desired reults, and I am able to continue getting hands on and implementing new changes.
Although not mentioned explicitly, the concepts of defense in depth, least-privilege, assume breach, and zero trust models will most likely be present in an enterprise environment. Implementing these concepts will help prevent attacks and mitigate them if needed. This also goes hand in hand with ACLs and ACEs that can be configured for the same purpose. Ensuring users have access to what they need, and only what they need is an important concept that, if implemented correctly, can greatly benefit an organization.

Overall this was a large undertaking but served its purpose as far as showing interest, initiative, willingness to learn, and understanding / importance of

  - Active Directory
  
  - Enterprise environments containing multiple domains
  
  - Trusts
  
  - Active Directory permissions, ACLs, and ACEs
  
  - Knowledge of Active Directory Best Practices
  
  - Troubleshooting and fixing Active Directory Hygiene related issues









