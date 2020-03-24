# Questions and answers

## Date : 04 Nov 2019

Question  | Answer
---|---
What is the billing cycle for machines and FaaS  |   In the compare document it compares the costs for this and it relates to how many calls to the function are made each plan has so many free and then you start paying
How long are the trial accounts for that we create in class   |  One month with over $100 
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
How do we trigger a fail of a "site" in Azure to test DR | Azure Traffic manager has the ability to setup access to dirrerent regions and through this you could have a failover strategy. 
How do we use expressroute for uploading information into office 365   |  The subscription cost covers this
What is a use case for the local storage emulator  |  When developing a solution using an on-prem storage emulator is fast cheap and provides most of the features developers would need to test out a solution
***Azure Account locked during course*** | Enter phone number and repond with SMS code to unlock
***If Azure account lock and you cannot unlock with sms code*** |  Go to [account.live.com](account.live.com) - in here there when logging in it will ask for your login and your phone number, a test is sent to you phone number and this will unlock the account. This fix is for when the login is telling you that the account is locked with to many retries.

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
What does an Azure lock, lock?|The lock placed on a parent scope is inherited by all resources within that parent scope, this applies to existing and newly created resources in that parent scope. [Azure Locks](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-lock-resources)
Who can remove an Azure lock?|To create or delete management locks, you must have access to Microsoft.Authorization/* or Microsoft.Authorization/locks/* actions. Of the built-in roles, only Owner and User Access Administrator are granted those actions.
What if I cannot remove the resource or the lock | Some Azure services, such as Azure Databricks, use managed applications to implement the service. In that case, the service creates two resource groups. One resource group contains an overview of the service and isn't locked. The other resource group contains the infrastructure for the service and is locked.<BR> - If you try to delete the infrastructure resource group, you get an error stating that the resource group is locked. If you try to delete the lock for the infrastructure resource group, you get an error stating that the lock can't be deleted because it's owned by a system application. <BR> - Instead, delete the service, which also deletes the infrastructure resource group.
Tag usage| Tags can be used for many purpose: Access Control and Compliance information, Automation tasks, Costing Information, Which resources are needed for generating reports. <BR>However do not have inconsistent tag data, example Department:HumanResources vs Department:HR this will create blindspots in your management and reporting. 
Page Blobs what are they good for| Page blobs are a collection of 512-byte pages, which provide the ability to read/write arbitrary ranges of bytes. Hence, page blobs are ideal for storing index-based and sparse data structures like OS and data disks for Virtual Machines and Databases [MS Docs](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blob-pageblob-overview)

## Date : 19 Dec 2019

Question  | Answer
---|---
Is there any way to backup the metadata of non-vm resources from Azure so that we can restore resources to their original state|This is the wrong way to look at resources in cloud, we should be looking to use IaC (Infrastructure as Code), cloud should be modified by idempotent, not procedural, changes. In this way if a resource needs to be re-added we run the idempotent IaC to replay the creation of the resource. 

## Date : 28 Jan 2020

Question  | Answer
---|---
Can we move resources from region to region? | [Move/Migrate Resources from one region to another](https://docs.microsoft.com/en-us/azure/site-recovery/azure-to-azure-tutorial-migrate)
Are Availabilty sets available in all subscription tiers? | There seems to be no information showing that this service is restricted to a set of tiers
How to find the difference between Azure VM family types, some look identical but have different prices? | [Different Azure Families](https://azure.microsoft.com/en-gb/pricing/details/virtual-machines/series/)
Is there a way to determine if a resource creation has finished when deploying with powershell? | [One way to be notified](https://docs.microsoft.com/en-us/azure/azure-monitor/platform/alerts-activity-log#create-with-azure-portal)
DSC is it installed automatically, or do we need to trigger the install with the UPDATE button | Azure Automation **State Configuration** brings the same management layer to PowerShell Desired State Configuration as Azure Automation offers for PowerShell scripting. [State Configuration](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-overview)


## Date : 29 Jan 2020

Question  | Answer
---|---
Moving blobs between cold and hot starage, what is the deal here. AWS just changes policies on s3 buckets, how does Azure do it? | The Set Blob Tier operation sets the access tier on a blob [Blob storage inforamtion](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blob-storage-tiers?tabs=azure-portal)
DNS Zone, Record Sets are they like DNS Round Robin? | The do not appear to be, most of the documentation I can find shows that most record sets consist of one record. I would guess that if the client can understand and use multiple answers from DNS then this would be useful. 

## Date : 29 Jan 2020

Question  | Answer
---|---
Can we create a VNet peer between subscriptions? | [YES](https://docs.microsoft.com/en-us/azure/virtual-network/create-peering-different-subscriptions) we can network peer between subscriptions

## Date : 30 Jan 2020

Question  | Answer
---|---
When tracking the routes to the Azure SQL server the lab says you should see no hops, we see 20 what are we seeing here |
Does Azure use its own provider for SMS? | [Pricing for mobile services](https://azure.microsoft.com/en-us/pricing/details/mobile-services/)
Load balancer basic - can it only LB Basic SKU NICs? | Virtual Machine Scale Sets/V must be in same location as Load Balancer. Only IP configurations that have the same SKU (Basic/Standard) as the Load Balancer can be selected. All of the IP configurations have to be in the same Virtual Network. [All the specs on the two SKUs](https://docs.microsoft.com/en-us/azure/load-balancer/concepts-limitations#publicloadbalancer)
Load balancer basic - can it only LB Basic SKU NICs? | Virtual Machine Scale Sets/Virtual Machines must be in same location as Load Balancer. Only IP configurations that have the same SKU (Basic/Standard) as the Load Balancer can be selected. All of the IP configurations have to be in the same Virtual Network. [All the specs on the two SKUs](https://docs.microsoft.com/en-us/azure/load-balancer/concepts-limitations#publicloadbalancer)
Can we run with Pass-thru Auth and Federation at the same time | It appears that you need to choose which Auth system you will use, this would mean you will use one or the other. [Doc showing choices for Auth](https://docs.microsoft.com/en-us/azure/security/fundamentals/choose-ad-authn)

## Date : 31 Jan 2020

Question  | Answer
---|---
What is the differences between the storage replication options | look [here](http://vunvulearadu.blogspot.com/2019/08/azure-storage-tiers-and-availability.html) 
How do CDNs get chosen in azure for contentdelivery |

## Date : 25 Mar 2020

Question  | Answer
---|---
If a resource gets created by PowerShell or Az command is there a way to track the creation progress in the portal |
