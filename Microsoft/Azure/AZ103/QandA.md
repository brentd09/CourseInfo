# Questions and answers

## Date : 04 Nov 2019

Question  | Answer
---|---
What is the billing cycle for machines and FaaS  |   In the compare document it compares the costs for this and it relates to how many calls to the function are made each plan has so many free and then you start paying
How long are the trial accounts for that we create in class   |  One month @ $140
Using Resource Groups for billing  |  Yes you can do this, the best way I have seen to do this is with a "BillTo" Tag on resources
Costs for Un-deallocated VMs  | [Stopped v deallocated](https://blogs.technet.microsoft.com/uspartner_ts2team/2014/10/10/azure-virtual-machines-stopping-versus-stopping-deallocating/) VMs core price will still be charged for un-deallocated
Getting "Subscription Is Not Registered " errors    |  [Subscription Is Not Registered](https://aidanfinn.com/?p=21192) web site to solve some of these errors
When creating a subscription there is a dev/test option what does this do? What are the costs?  |  [Dev/test labs](https://azure.microsoft.com/en-au/pricing/details/devtest-lab/) This website shows what is free and paid services for test/dev
When running the Powershell in the lab there was an Authentication error    |  We solved this by logging off and on (the portal) 
Step 10 Task 3, need to create a **NEW** resource group  | Make sure the students hit the New link under the resource group box  
The Extensions seems to work but the web server was not active   | re ran extensions twice and then worked 

## Date : 05 Nov 2019

Question | Answer
---|---
How do we trigger a fail of a "site" in Azure to test DR    |  I think this requires a different mindset as we can have a failover to another region but within our region we don not have failover sites like we do on-prem.
How do we use expressroute for uploading information into office 365   |  The subscription cost covers this
What is a use case for the local storage emulator  |  When developing a solution using an on-prem storage emulator is fast cheap and provides most of the features developers would need to test out a solution
Azure Account locked during course | Enter phone number and repond with SMS code to unlock
If Azure account lock and you cannot unlock with sms code |  Go to account.live.com - in here there when logging in it will ask for your login and your phone number, a test is sent to you phone number and this will unlock the account. This fix is for when the login is telling you that the account is locked with to many retries.

## Date : 06 Nov 2019

Question  | Answer
---|---
 How to trigger a RunBook manually |   [Start RunBook manually](https://docs.microsoft.com/en-us/azure/automation/start-runbooks) 
 Azure action - SMS how much does it cost | The creation of the Alert Action says that carrier charges may apply, when tested we saw it uses an Australian cellphone number   

## Date : 07 Nov 2019

Question  | Answer
---|---
Azure stack? What is this? | This is Microsoft's answer to OpenStack,   Azure Stack is basically the same APIs, tools and processes that power Azure, but it’s intended to be hosted on-premises in private cloud scenarios. This started as a software platform and now is available as hardware solutions.<BR>[Azure Stack Intro](https://channel9.msdn.com/Blogs/azurestack/Introducing-Microsoft-Azure-Stack?term=azure%20stack&lang-en=true)
Azure Arc | Organize and govern across environments - Get databases, Kubernetes clusters, and servers sprawling across on-premises, edge and multicloud environments under control by centrally organizing and governing from a single place. Utilising the power of Azure Stack.
How to move a VM to another region | [Move Azure VM to another region](https://docs.microsoft.com/en-us/azure/site-recovery/azure-to-azure-tutorial-migrate)
How are load balancer highly available | Load balancers are regionally based so it would take a region outage to lose a load balancer

## Date : 16 Dec 2019

Question  | Answer
---|---
What does an Azure lock, lock?|The lock placed on a parent scope is inherited by all resources within that parent scope
Who can remove an Azure lock?|To create or delete management locks, you must have access to Microsoft.Authorization/* or Microsoft.Authorization/locks/* actions. Of the built-in roles, only Owner and User Access Administrator are granted those actions.
