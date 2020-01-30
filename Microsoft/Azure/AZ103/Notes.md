

# Module 0 Welcome





Professionals how to manage 





Azure Active Directory, 

This is a note



# Module 1 Azure Administration





Resource Group Deployments

- You can track for success or failure to deploy a resource to a Resource Group 

Public note added a month ago by Brent Denny





Resource Manager Locks

- Prevents accidental deletion of a resource Two types - Read-Only Lock - prevents any change to the resource - Delete Lock - prevents the deletion Only Owners and Access Admin can manage Locks





Moving Resources

Can move resources to either - a new subscription - a new resource group in the same subscription Source group and the Target group are locked during the operation





Removing Resources and Resource Groups

BE CAREFUL - Deleting a Resource Group - Deletes all of the resources contained within it Resources my be dependencies for other Resources in other groups - understand the dependencies before deleting - Creating all of the resources that are related by dependencies may be a good idea





Template Advantages

- Repeatable resource creation - Define dependent resources - Reduce errors - Faster to deploy - Infrastructure As Code - Link templates to make them modular





Template Parameters





Template Variables





QuickStart Templates





specify which values are configurable when the template runs. 





define values that are used throughout the template. 





templates provided by the Azure community.





Write and delete operations are blocked on the resource groups until the move completes. 





Locks are inherited by child resources.





Resource Manager template can contain sections 





template benefits 





Just because a service can be moved doesn’t mean there aren’t restrictions. 





can move a virtual network, but you must also move its dependent resources, like gateways.





Guidance for creating resource groups





Functionality initially released through APIs 





represented in the portal within 180 days 





Values that are provided when deployment is executed to customize resource deployment.





When creating a resource group, you need to provide a location for that resource group. 





resource providers. 

Get-AzResourceProvider | Select-Object -Property ProviderNamespace

Public note added a month ago by Brent Denny





The resource group stores metadata about the resources. Therefore, when you specify a location for the resource group, you're specifying where tha [...]





can link Resource Manager templates together to make the templates themselves modular. 



# Module 2 Azure Virtual Machines





Location and Pricing

- Must select a location/Region Two costs - Compute - priced by hour, billed by the minute - Storage - regardless of machine state, storage billing is priced on disk storage Two payment options - Consumption - Reserved Instances - can be over 70% reduced cost, if you terminate early the RI can be transferred or refunded





Virtual Machine Sizing





Virtual Machine Disks

Azure VMs have at least 2 disks: - OS Disk - Managed - See next page in book for 'Managed Disk' description - Temp Disk - Intended to only store data such as page or swap files it is non managed Other disks can be added for storge - VHDs - Max capacity 4095 GiB - Managed





Storage Options

https://docs.microsoft.com/en-us/azure/virtual-machines/windows/managed-disks-overview 

Public note added a month ago by Brent Denny





Supported Operating Systems

Operating Systems - Choice of OS will influence the cost - Windows - Linux - Centos - CoreOS, Debian, OracleLinux, RHEL, Ubuntu Azure MarketPlace - Apps - Licenses are metered out by azure for some software, others you have to obtain yourself 





Creating Virtual Machines in the Portal

The New VM Portal will guide you through these steps: Basic - Project details - Administrator account - Inbound port rules Disks - OS disk type - data disks Networking - Virtual networks - load balancing Management - Monitoring - Auto-shutdown - Backup Guest config - Add additional configuration - agents - scripts , etc.





Windows Virtual Machines

2019 Releases: LTSC 5 years support 5 years Extended support SAC are released every 6 months (supported for 18 months) 2016 and 2012 are also available





Windows VM Connections

Remote Management of an Azure VM RDS WinRM - for WinRM - need to also setup (KeyVault, Certificate, Add Cert to KeyVault, Locate the URL of uploaded cert, Ref the URL in the AzureVM Configuration)





Linux Virtual Machines

- Many Linux images in the Azure Marketplace. - Linux has the same deployment options as for Windows - You can manage your Linux with Puppet, and Chef





Linux VM Connections

Connect remotely to Linux VM via SSH Auth: - username - SSH public key OR password





Maintenance and Downtime

Unplanned Hardware Maintenance - Azure platform predicts that the hardware or any platform component associated to a physical machine, is about to fail. - Azure uses Live Migration technology to migrate the VMs from the failing hardware to a healthy physical machine Unexpected Downtime - when the hardware or the physical infrastructure for the virtual machine fails unexpectedly. Planned Maintenance - periodic updates made by Microsoft to the underlying Azure platform





Availability Sets

Fault Domains & Update Domains - described on next page





Update and Fault Domains

Each virtual machine in an availability set is placed - in one update domain - During planned maintenance, only one update domain is rebooted at a time. and - in two fault domains - A group of virtual machines that share a common set of hardware, switches and share a common single points of failure





Availability Zones

Regions are made up of - Unique physical locations - one or more datacenters - three zones - different locations - zone redundant service - replicate the service and data to other zones in the region - zonal service - Pins the service to a Zone





Scale Sets

As demand goes - up - more virtual machine instances can be added, - down - virtual machines instances can be removed. The process can be - manual - automated - combination of both.





Implementing Scale Sets

Instance count - (0 to 1000). Instance size. - The size of each virtual machine in the scale set. Deploy as low priority. - Can save up to 80% over usual on-demand costs. - Low priority is not available for all selected sizes. Use managed disks. - Managed disks hide the underlying storage accounts and instead shows the abstraction of a disk. Enable scaling beyond 100 instances. - If No, the scale set will be limited to 1 placement group ,max capacity of 100. - If Yes, the scale set can span multiple placement groups. Capacity to be up to 1,000 A proximity placement group - is an Azure Virtual Machine logical grouping capability that you can use to decrease the inter-VM network latency associated with your applications. - When the VMs are deployed within the same proximity placement group, they are physically located as close as possible to each other.





Implementing Autoscale

Not setting this up correctly could be very costly - if there is an Attack on your VMs that puts extra load on the VMs this might drive the instances up - An issue with an app triggers the scaling accidently





Custom Script Extensions

Can install the CSE from the Azure portal by accessing the virtual machines Extensions blade Run PowerShell commands on the VM





Azure Virtual Machine creation checklist





Premium Storage 





Desired State Configuration





high-performance, low-latency disk support 





automatically launch 





should also define a minimum, maximum, and default number of VM instances. 





related VMs are deployed so that they aren't all subject to a single point of failure 





first decisions is the image to use. 





customization tasks post configuration. 





unique physical locations within an Azure region.





Windows 





datacenters are grouped into geographic regions (





All Azure virtual machines have at least two disks 





Linux. 





there are several ways to automate the tasks of creating, maintaining, and removing virtual machines. 





solid-state drives (SSDs). 





made up of one or more datacenters 





Benefits of autoscale





not all upgraded at the same time 





operating system disk (





Additional images are available by searching the Marketplace.





upgrade domain (





temporary disk. 





minimum of three separate zones in all enabled regions.





nodes that are upgraded together 





You can install the CSE from the Azure portal by accessing the virtual machines Extensionsblade. 





more than just base OS 





additional configuration 





should perform an identical set of functionalities and have the same software installed.





RDP)





small applications that provide post-deployment configuration and automation tasks on Azure VMs. 





The physical separation of Availability Zones within a region protects applications and data from datacenter failures.





can save up to 80% over usual on-demand costs. 





can search the Azure Marketplace for more sophisticated install images 





lets you place your VMs as close as possible to your users to improve performance 





VMs in the scale set may be evicted at any time. 





up to 256 TB of storage per VM. 





ensures 





VMs 





Zone-redundant services replicate your applications and data across Availability Zones 





best way to determine the appropriate VM size is to consider the type of workload 





run across multiple physical servers, compute racks, storage units, and network switches. 





VMs and services that are 





meet any legal, compliance, or tax requirements.





part of the same virtual network can access one another. 





Availability Zones, Azure offers industry best 99.99% VM uptime 





throughput of up to 2,000 megabytes per second (





Azure VM extensions can be:





location can limit your available options





Availability Zone 





Managed 





CLI, 





PowerShell, 





combination of a fault domain and an update domain. 





All VM instances are created from the same base OS image and configuration. 





Resource Manager templates, 





Once the file is uploaded it executes immediately.





Azure portal.





allow access to the external service, including your on-premises servers.





price differences between locations





Enable scaling beyond 100 instances.





not a managed disk. 

https://docs.microsoft.com/en-us/azure/virtual-machines/windows/managed-disks-overview Ensures - Availability - the assurance of uptime - Durability - the assurance of data integrity

Public note added a month ago by Brent Denny





unmanaged disks. 





fault domain (





keep these principles in mind.





support the use of the Azure load balancer 





you can create your disk image 





physical unit of failure. 





upload it to Azure storage, 





different extensions for Windows and Linux 





common set of hardware, switches, that share a single point of failure. 





stored as page blobs in Azure storage accounts.





Things to consider





DSC script consists of the following:





Azure only supports 64-bit 





Custom Script extensions have 90 minutes to run. 





multiple instances of your application. If one of these VM instances has a problem, customers continue to access your application through one of t [...]





An Azure managed disk 





we will focus 





virtual hard disk (VHD). 





Custom Script Extensions 





Desired State Configuration. 





cases where the data may not persist, 





WinRM)





based on PowerShell.





expenses are priced on a per-hour basis but billed on a per-minute basis. 





virtual machines include a license for many common products 





Zonal services 





data on the temp drive should not be data that is critical to the system.





pin the resource to a specific zone (





two or more instances deployed across two or more Availability Zones in the same Azure region, 





requires networking or storage access, make sure that content is available.





Zone-redundant 





replicates automatically across zones (





name of up to 15 characters on a Windows VM and 64 characters on a Linux 





account for any errors that might occur when running your script. 





Connectivity to at least one instance at least 99.99% of the time.





support up to 1,000 VM instances. 





two or more instances deployed in the same Availability Set, 





The cost for a VM includes the charge for the Windows operating system. 





own custom VM images, the limit is 300 VM instances.





Don’t store data on the temporary disk. 





extension may need sensitive information 





Connectivity to at least one instance at least 99.95% 





Make a note of your login information including user and public IP address.

Go into networking and add a port rule to allow TCP22 inbound





How will you protect/encrypt this information?





Single Instance Virtual Machine using premium storage for all Operating System Disks and Data Disks, 





charged separately for the storage 





data disk is a managed disk 





best performance 





Linux distributions 





Azure allows you to change the VM size when the existing size no longer meets your needs. 





CentOS by OpenLogic, Core OS, Debian, Oracle Linux, Red Hat Enterprise Linux, and Ubuntu.





migrate any VM disk that requires high IOPS to Premium Storage. 





Connectivity of at least 99.9%.





two payment options 





Consumption-based





Managed disks are required 





pay for compute capacity by the second. 





For example, devusc-webvm01





virtual machine SLA (99.95%).





Be cautious when resizing production VMs - they may need to be rebooted 





Reserved Virtual Machine Instances





commitment is made up front, 





72% price savings 



# Module 3 Azure Storage





Azure Storage

https://channel9.msdn.com/events/Build/2018/BRK2112?term=%22azure%20storage%22&sortBy=recent&lang-en=true&pageSize=15 Availability - Resource up time Durability - Long term data integrity Secure - All data wriiten to Azure storage is encryted Scalable. Designed to be massively scalable Managed. Azure handles all of the - hardware maintenance - updates - critical issues Accessible. Accessible from anywhere in the world over HTTP or HTTPS. Can store - files - messages - tables - other types of information Categories of data stored: - VM Storage - Unstructured Data. - Blobs (Blobs are highly scaleable) - Data Lake Store (is an Hadoop Distributed File System (HDFS)) - Structured Data - Tables (Key-Value pairs) - CosmosDB - SQL DB

Public note added a day ago by Brent Denny





Azure Storage Services

Blob - Optimsed for massive unstructured data - Text and binary object - Access via HTTP/S Azure Files - Can set up highly available network file shares - Accessed from anywhere by SMB or REST interface - Supports R/W from multiple machines - Accessed using a URL that points to the file and includes a shared access signature (SAS) token - (Not supported YET) - Active Directory-based authentication and access control lists (ACLs) Queue - Stores messages in queues to be processed sequentially - (https://www.youtube.com/watch?v=Tu9WGaePtBA) Table - Table storage is now part of Azure Cosmos DB.





Storage Account Types

https://docs.microsoft.com/en-us/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs 





Accessing Storage

Every "object" stored in Azure Storage has a unique URL 





Demonstration - Creating Storage Accounts

https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blob-soft-delete?tabs=azure-portal





Azure Storage Explorer

https://azure.microsoft.com/en-gb/features/storage-explorer/





Blob Containers

- Unlimited number of containers - No Nested folders by default - however this site will show you how nesting can be done (https://fsou1.github.io/Nested_folders_with_azure_blob_storage/)





Blob Performance Tiers

https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blob-storage-tiers - If the data is not kept in storage for the "at least time" then you will be hit with an early deletion fee Hot - Optimised for frequent access Cool - store large amouts of data that are access infrequently Archive - retrieval have have hours of latency - Cheap storage - expensive retrieval 





Uploading Blobs

Block blobs - blocks of data assembled to make a blob. - Most scenarios using Blob storage employ block blobs. - Ideal for storing text and binary data in the cloud, like files, images, and videos. Append blobs - like block blobs in that they are made up of blocks - but they are optimized for append operations - so they are useful for logging scenarios. Page blobs - can be up to 8 TB in size - more efficient for frequent read/write operations - can retrieve arbitry blocks of data - Best use for page blobs is OS and Database storage.





Azure Files

https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows#using-an-azure-file-share-with-windows 





Files vs Blobs

Files - File shares in the cloud - access by SMB - Folders Blob - access via http/s - REST accessible - Flat directory structure 





Secure Transfer Required

Can set secure or not on Blob storage however SMB requires secure connections





Storage Security





Shared Access Signatures

Give to clients that you dont trust with Access Key - Access to: - blob - file - queue - table - Give time frame that the SAS can be valid for - give specific permissions Read and Write but NOT Delete (for example) - cannot modify SAS settings (immutable) Two types - Account - gives access to one or more storage services - Service - gives access to only one resource (blob , queue, table or file)





Configuring SAS Parameters

This uses one of the access keys only to generate the SAS token - the access-key is not required on the client - restrictions of time - permission - IP range and protocol can be configured





URI and SAS Parameters

When Creating the SAS a URI is also created - The URI consists of your Storage Resource URI and the SAS token





Storage Service Encryption

Encrypts data at rest (256-bit AES encryption) it to: Decrypts the data before retrieval. Enabled for all new and existing storage accounts - encryption cannot be disabled - Can use own key for encryption





Customer Managed Keys

Azure Key Vault to manage your keys, secrets, certificates Region specific - need to create new key vault per region where secrets are needed





Every object 





container provides a grouping of a set of blobs. 





stored access policy 

Access Keys - Give access to the storage account SAS - gives fine grained access to objects - once created you cannot edit them ##Stored Access Policies## - is the third option, this can supply editable access to the container level 





storage accounts use a pricing model for blob storage based on the tier of each blob. 





Files offers fully managed file shares 





access your files, you will need a file share. 





shared access signature (SAS) 





When you use shared access signatures 





several types of storage accounts. 

https://docs.microsoft.com/en-us/azure/storage/common/storage-redundancy 





connect to your Azure file share with Windows or Windows Server. 





you can use the Azure Key Vault to manage your encryption keys. 





several ways to connect 





capability to take share snapshots of file shares. 





standalone app 





URI that grants restricted access rights to Azure Storage resources (





Linux distributions using the CIFS kernel client. 





supports different features 





storage account name 





two potential risks:





object store for data objects, a file system service for the cloud, a messaging store for reliable messaging, and a NoSQL 





Server Message Block (SMB) 





subdomain 





accounts associated with your Azure subscriptions.





Blobs





unlimited number of containers. 





SAS is leaked, it can be used by anyone 





Portal)





object 





billing considerations 





accounts and services that are shared from other Azure subscriptions.





example URI. 





Files





file shares for cloud 





Azure Storage is:





manage local storage 

https://docs.microsoft.com/en-us/azure/storage/common/storage-use-emulator How the storage emulator works The storage emulator uses a local Microsoft SQL Server 2012 Express, LocalDB instance to emulate Azure storage services. You can choose to configure the storage emulator to access a local instance of SQL Server instead of the LocalDB instance. The storage emulator connects to SQL Server or LocalDB using Windows authentication.





SAS provided to a client application expires 





Queues





Encryption





if your storage account is 





Common uses of Blob storage 





Retrieval is provided at the individual file level, 





Storage account type

https://docs.microsoft.com/en-us/azure/storage/common/storage-account-overview





ensures that your data is safe in the event of transient hardware failures. 





reliable messaging between application 





mystorageaccount





images or documents 





components.





Replication options

Locally redundant storage (LRS): Low-cost data redundancy for Azure Storage Zone-redundant storage (ZRS): Highly available Azure Storage applications Geo-redundant storage (GRS): Cross-regional replication for Azure Storage Geo-zone-redundant storage (GZRS) for highly availability and maximum durability (preview) - https://docs.microsoft.com/en-us/azure/storage/common/storage-redundancy





Tables





endpoints for your storage account are:





NoSQL store 





files for distributed access, 





cannot delete a share that has share snapshots unless you delete all the share snapshots first.





Authentication





Block blobs are ideal for storing text and binary data in the cloud, like files, images, and videos.





frequent access 





application's functionality may be hindered.





blob.core.windows.net





video and audio.





Recommendations





data for backup and restore, 





object storage solution 





table.core.windows.net





rules for file service share 





storage resources support stored access policies:





Public access level





snapshots are incremental 





can help mitigate these risks:





queue.core.windows.net





data for analysis 





The following features are present in the latest version of Storage Explorer.





information is available by selecting 





access policy 





file.core.windows.net





Common uses of file storage 





Connectfrom your file share page.





Blob storage offers three types of resources:





can be associated 





SAS gives you granular control over the type of access you 





minimizes the time required to create the share snapshot 





optimized for append operations, 





shared access signature 





data written to Azure 









Provides an SMB interface, 





Storage is encrypted 





grant to clients who have the SAS, 





no anonymous access 





replace or supplement traditional on-premises file servers 





Azure Files will reject SMB 2.1 (or SMB 3.0 without encryption). 





naming restrictions for shares are as follows:





Blob





stored for at least 30 





stored access policy on a 





delegate access 





General-purpose v2 accounts (StorageV2)

General-purpose v2 storage accounts support - the latest Azure Storage features - incorporate all of the functionality of general-purpose v1 - (Dec 2019 Microsoft Docs) - https://docs.microsoft.com/en-us/azure/storage/common/storage-account-upgrade?tabs=azure-portal





allow anonymous public read 





to multiple storage services. 





to access myblobin the mycontainer





days. 





share can be associated with a shared access signature 





more efficient for frequent read/write operations. 





blob, file, queue, and table.





Container





Data in transit





designed to be 





http://mystorageaccount.blob.core.windows.net/mycontainer/myblob.





allow anonymous public read and list access to the entire container, 





granting permissions to the share itself or to the files it contains. 





massively scalable 





Recommended 





When to use share snapshots





most scenarios using Azure Storage.





Configuring a Custom Domain

Direct CNAME mapping - The first, and simplest, method is to create a canonical name (CNAME) record that maps your custom domain and subdomain directly to the blob endpoint. - Maps a source domain to a destination domain. - example, the source domain is your own custom domain and subdomain www.contoso.com - mystorageaccount.blob.core.windows.net Intermediary mapping with asverify - The second method also uses CNAME records. - To avoid downtime, however, it first employs a special subdomain asverify that's recognized by Azure. Mapping your custom domain to a blob endpoint can cause a brief period of downtime while you are registering the domain in the Azure portal. If the domain currently supports an application with a service-level agreement (SLA) that requires zero downtime blobs.contoso.com - contosoblobs.blob.core.windows.net asverify.blobs.contoso.com - asverify.contosoblobs.blob.core.windows.net Azure needs to verify that you can alter the zone asverify shows you have.





Protection against application error and data corruption





start time and the expiry time.





data that is transferred out of an Azure region) 





permissions granted by the SAS. 





HTTPS, or SMB 3.0.





Azure handles hardware maintenance, updates, and critical issues for you.





easy to “lift and shift” applications to the cloud that expect a file share 





Disk encryption





might grant read and write permissions to that blob, but not delete permissions.





accessible 





Archive tier for at least 





Blob upload tools





Azure Disk Encryption.





Shared Access Signatures





Optionally, you can 





HTTP or HTTPS. 





180 days. 





multiple methods to upload data to blob storage, 





Azure File shares can also be replicated with Azure File Sync to Windows Servers, 





REST interface that allows unstructured data to be stored and accessed 





Specify an IP address or range of IP addresses 





access to the data 





can be granted using Shared Access Signatures.





which Azure Storage will accept the SAS. 





NET, Java, Node.js, Python, PHP, Ruby, Go, and others 





PowerShell)





REST API. 





set up highly available network file shares 





protocol over which Azure Storage will accept the SAS. 





Storing shared application settings, 





diagnostic data such 





logs, metrics, 





Protection against accidental deletions or unintended changes





two types of SAS: 





Storing 





tools 





Factory

https://azure.microsoft.com/en-au/resources/videos/azure-data-factory-overview/ Process different types of data automatically at scale - Consume, Orchestrate and transform data - analyse the process

Public note added a month ago by Brent Denny





Direct CNAME mapping





utilities needed for developing or administering Azure virtual machines or cloud services.





store files, messages, tables, and other types of information. 





account 





access to resources in one or more of the storage services. 





Azure AD)





service SAS 





resource in just one of the storage services: 





access your existing block blob data 





General backup purposes





through the Linux file system.





Shared Key authorization 

Not a good idea, if the holder of the key is no longer affiliated with you, they still can access the storage. - you would need to cycle the access keys - causing all the other apps relying on access keys to FAIL 





Data Box 

https://azure.microsoft.com/is-is/services/databox/

Public note added a month ago by Brent Denny





Intermediary mapping with asverify

https://docs.microsoft.com/en-us/azure/storage/blobs/storage-custom-domain-name Azure need to be able to determine that you are able to modify the DNS zone, the ASVERIFY reference understood by azure, tells azure that you have that ability 

Public note added 2 days ago by Brent Denny





think of Azure storage in three categories.





Storage for Virtual Machines





used for many common scenarios:





on-premises applications use file shares. 





makes it easier to migrate those applications 





specified permissions and over a specified time 





Unstructured Data





includes Blobs 





Data Lake Store. 

big data analytics





export large amounts of data from your storage account 





Configuration files can be stored on a file share and accessed from multiple VMs. 





Structured Data. 





to hard drives 





anonymous read access. 





Microsoft then ships back to you with your data.





examples maps a domain to the Azure storage account in DNS with the asverify intermediary domain:





storage accounts have two tiers: 

Storage accounts have two tiers: Standard - HDD - Slower - Cheaper Premium - SSD - Faster - More expensive No Coversion available in either direction





Diagnostic logs, metrics, and crash dumps 





Standard





magnetic drives (





Premium





solid state drives (





not possible to convert a Standard storage account to Premium storage account or vice versa. 





Queue storage

MS tells of an example where they are accepting a picture for someones account, The web site does not put restrictions on the exact size for the picture, - the picture will need to be queued because the app needs to resize the picture before implementing it. - So it is placed in storage queue, - the resizing app requests the picture from the queue, - which in turn marks the picture as hidden in the queue for a time period, while the resizing is done. The resize app can ask for more time from the queue, or tell the queue that the jobs is done so the original image can be removed





used to store and retrieve messages. 





a queue can contain millions of messages. 





Azure Table storage is now part of Azure Cosmos DB. 

Azure NoSQL offering - Cosmos DB



# Module 4 Virtual Networking





Virtual Networks

VNets - Isolated CIDR address block - Routing is automatic to any subnets in the Vnet - Subnets are created as subnets of the Vnet - Can use VPNGateway to connect the Vnet to other networks including OnPrem - IPSEC secure connection





Subnets

Each subnet you create: (5 addresses are used by Azure / subnet) - /29 is the smallest subnet - /29 - 3 usable host address + 5 Azure host addresses = 8 total ips Reserved IPs: - x.x.x.0: Network address - x.x.x.1: Reserved by Azure for the default gateway - x.x.x.2, x.x.x.3: Reserved by Azure to map the Azure DNS IPs to the VNet space - x.x.x.255: Network broadcast address Network Security Groups - can also applied to subnets - Like firewalls





Implementing Virtual Networks

Implement address pool for VNet and at least ONE Subnet Be careful not to overlap addresses with other network - Overlapping networks will cause issues when you attempting to connect these networks





Multiple NICs in Virtual Machines

NIC names may change on Azure updates - but IP and MAC will remain the same To Add or remove NIC you must deallocate VM first All NICs in a VM must be in the same VNet The Default NIC is the NIC that has the EXTERNAL IP assigned





IP Addressing

Public IP - Dynamic - IP is given for the life of the VM, unless deallocated - Static- Never changes or released - Used when needing Certificates to a VM service - Basic SKU - All inbound traffic allowed - NSG blacklist traffic - Standard SKU - All inbound traffic blocked - NSG whitelist traffic - Used - Access tp internet - External facing Azure resources Private IP - Dynamic - IP is given for the life of the VM, unless deallocated - Static- Never changes or released - Basic SKU - All inbound traffic allowed - NSG blacklist traffic - Standard SKU - All inbound traffic blocked - NSG whitelist traffic - Used - Access 





Service Endpoints

Normally the resources on you network try to use the external IP as the source to access the Azure service, Service endpoints - Stop external traffic from hitting the Azure Services that can use Service Endpoints - limit how the Service can be accessed - potentially improve security 





Service Endpoint Services

Tie a certain service to a subnet or subnets. The External access to that service will be stopped. https://www.youtube.com/watch?v=ic6Laiv9Jfc

Public note added a month ago by Brent Denny





Secure Access to Storage Endpoints





Domains and Custom Domains

Initial Domain - .domainname.onmicrosoft.com Notes - Only a global administrator can perform domain management - Domain names in Azure AD are globally unique. Before a custom domain name can be used by Azure AD, - must be added - must be verified that you own it.





Verifying Custom Domain Names

To verify that you own a domain test for a: - txt record - MX record





Azure DNS Zones

Allows you to resolve names without having to setup a whole IaaS DNS solution When doing so remember: - The name of the zone must be unique within the resource group - and the zone must not exist already. - The same zone name can be reused in a different resource group OR different Azure subscription. - Where multiple zones share the same name - each instance is assigned different name server addresses. - Only one set of addresses can be configured with the domain name registrar.





DNS Record Sets

You add records and record sets the same way - click + Record Set - Record - stop at one IP - Record Set - Keep adding IPs for the same name (Max 20)





DNS for Private Domains





When configuring Private Domain "Registration": - Forward A records are automatically created - Reverse PTR records are also created for the registering VMs - You can MANUALLY add other records - A - AAAA - CNAME - MX - PTR - SRV - TXT Split-Brain DNS is created by - creating a Private DNS Zone and a DNS zone (public) with the same domain name - setup duplicate host names with different IPs - (Internal IP on Private Domain and Public IP on DNS Domain)





Network Security Groups

Sets up rule to allow or deny traffic Can be associated with: - Subnet - Interface ACLs and NSG cannot coexist! Limits - 100 NSGs / Region/ Subscription - 200 Rules / NSG Do NOT apply NSGs to VPN Gateways or ExpressRoute Subnets - this will block the traffic flow





NSG Effective Rules

If NSG Rules are placed on the Subnet and Interface they both have to allow traffic before it can enter the PC on that subnet





virtual network 





public IP address resource can be associated with 









is easy to add a service endpoint to the virtual network. 





is easy to add inbound and outbound rules. 





limit network traffic 





when you want to apply NSG to both VM (NIC) and subnet 





segmented 





steps necessary to restrict network access to Azure services varies across services. 





one or more subnets. 





can be associated with 





virtual machine network interfaces, internet-facing load balancers, VPN gateways, and application gateways. 





using a network security group (





accessing a storage account, you would use the 





Azure Active Directory, Azure Cosmos DB, EventHub, KeyVault, Service Bus, SQL, and Storage.





There are two types of IP addresses 





Having multiple NICs is a requirement for many network virtual appliances, 





Firewalls and virtual networksblade to add the virtual networks that will have access. 





“allow” rule must exist at both levels 





variety of services such as HTTPS, RDP, FTP, and DNS.





application delivery and WAN optimization solutions. 





Service.





By default, you can create up to 50 virtual networks per subscription per region, 





public and private IP 









can add up to 20 records to any record set. 





multiple NICs also provides more network traffic management functionality, 





add 





rules by specifying 





Azure service traffic from a virtual network uses public IP addresses as source IP addresses. 





Name, Priority, Port, Protocol (Any, TCP, UDP), Source (Any, IP Addresses, Service tag), Destination (Any, IP Addresses, Virtual Network), and Act [...]





easiest way to locate the name servers assigned to your zone is through the Azure portal. 





can assign NSGs to subnets 





can increase this limit to 500 





create protected screened subnets (





service endpoints, service traffic switches to use virtual network private addresses as the source IP addresses when accessing the Azure service f [...]





Each 









VNet you create has its own CIDR block and can be linked to other VNets and on-premises networks if the CIDR blocks do not overlap. 





Port ranges.





carefully plan your subnets. 





create a public IP 





Azure assigns the next available 





order of the NICs from inside the VM will be random and could also change across Azure infrastructure updates. 





use an address space that is not already in use 

Even if you are not going to connect this address space to another, with overlapping addresses - you do not know what will be needed in the future - using a unique address space future proofs your configuration If you have overlapping addresses and need these networks to communicate you will need to reconfigure something





choice of either Basic or Standard.

https://docs.microsoft.com/en-us/azure/virtual-network/virtual-network-ip-addresses-overview-arm#ip-address-version

Public note added a month ago by Brent Denny





statically 





assign NSGs to a NIC 





dynamically 





Static IP addresses do not change and are best for certain situations such as:





traffic that flows through that NIC is controlled 





Why use a service endpoint?





However, the IP addresses, and the corresponding ethernet MAC addresses will remain the same. 





Improved security 





Basic SKU





Standard SKU





may require, or create, their own subnet, 





Azure has many networking components.





You select and assign 





Priority.





You can override Azure's default routing to prevent Azure routing between subnets, 





Optimal routing 





When delegating a domain to Azure DNS, you must use the name server names provided by Azure DNS. 





require that traffic between resources in the same virtual network flow through a network virtual appliance (NVA), 





consider when using multiple NICs.

To modify VMs to have multiple NICs - you must first deallocate the VM - then make the change Tested this 17Dec2019 - book is correct, - you can create the interface - but cannot attach it to the VM until it is down & de-allocated





can limit access to Azure resources 





such as an Azure storage account or Azure SQL database, to specific subnets with a virtual network service endpoint. 





If you want to set up a separate child zone, 





can delegate a sub-domain in Azure DNS. 





Keeping traffic on the Azure backbone network allows you to continue auditing and monitoring 





Simple to set up 





PowerShell example demonstrates how this works. 





network security group contains rules, which allow or deny traffic 

Like a firewall



# Module 5 Intersite Connectivity





VNet Peering

To Peer - One first VNet under settings - Peering - Choose other VNet to Peer to - All traffic is private in a peer - traffice is not sent over open networks - MS Backbone - low latency - high speed network - Once Peered the Vnets can route data to all the VNets subnets - To route on the peered backbone - use the internal IP of the resources





Gateway Transit and Connectivity

On the Peer you can enable this, It allows a peer to use a gateway to route data Therefore if three Vnets exist - you can use the GW from a peered Vnet - to access resources that are not peered directly to your vnet





Configure VNet Peering

Vnet routing: https://docs.microsoft.com/en-us/azure/virtual-network/virtual-networks-udr-overview Connects Vnets in the same region and allow routing between them - not transitive though - if just using peering - connections need to be made between each vnet pair Service chaining is a way to overcome the lack of transitivity

Public note added a month ago by Brent Denny





Service Chaining

https://docs.microsoft.com/en-us/azure/virtual-network/virtual-networks-udr-overview#user-defined VNet Peering is NOT transitive VNets have a limit of 10 Peers per VNet To solve these issues (without creating a direct peering): - User Defined Routes (Service Chaining) - Service chaining enables you to direct traffic from one virtual network to a virtual appliance or gateway in a peered network through user-defined routes. - To enable service chaining, configure user-defined routes that point to virtual machines in peered virtual networks as the next hop IP address. User-defined routes could also point to virtual network gateways to enable service chaining. - You can deploy hub-and-spoke networks, where the hub virtual network hosts infrastructure components such as a network virtual appliance or VPN gateway. All the spoke virtual networks can then peer with the hub virtual network. Traffic flows through network virtual appliances or VPN gateways in the hub virtual network. 

Public note added 2 days ago by Brent Denny





VNet-to-VNet Connections

Using this connection method, you create a VPN gateway in each virtual network. - A secure tunnel using IPsec/IKE provides the communication between the networks To same or different: - Regions - Subscriptions - Deployment models - In cloud to On Prem 





VPN Types





Gateway SKUs





Configure the On-Premises VPN Device

https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-devices

Public note added a month ago by Brent Denny





ExpressRoute Connections

https://docs.microsoft.com/en-us/azure/expressroute/expressroute-connectivity-models

Public note added a month ago by Brent Denny





VNet Peering is nontransitive. 





simplest and quickest way to connect your VNets is to use VNet peering. 





Before creating a virtual network gateway 





create a connection between your on-premises network and the Microsoft cloud in three different ways, 





ExpressRoute is a direct, private connection from your WAN (not over the public Internet) to 





VPN gateway is a specific type of virtual network gateway 





Microsoft has validated 





steps to configure VNet peering. 





steps to creating a VNet-to-VNet connections. The 





local network gateway typically refers to the on-premises location. 





list of standard VPN devices that should work well with the VPN gateway. 





first need to create the gateway subnet. 





dedicated private connection facilitated by a connectivity provider. 





send encrypted traffic between an Azure virtual network and an on-premises location 





can verify the connections either in the portal, or by using PowerShell.





gateway subnet contains the IP addresses that are used by the virtual network gateway. 





Cisco, Juniper, Ubiquiti, and Barracuda Networks. 





However, you can leverage user-defined routes and service chaining to implement custom routing that will provide transitivity. 





workloads, throughputs, features, and SLAs.





Point-to-Site (P2S) connection 





best to create a gateway subnet by using a CIDR block of /28 or /27 to provide enough IP addresses to accommodate future additional configuration [...]





your VNets can be:





connections fast, reliable, and private





same or different regions.





You can configure a Site-to-Site VPN as a secure failover path for ExpressRoute 





same or different subscriptions.





create private connections between Azure datacenters and infrastructure on your premises 





Each virtual network can have only one VPN gateway. 





same or different deployment models.





using. Site-to-Site (S2S) configurations 





address prefixes you specify are the prefixes located in the on-premises network.





Azure or on-premises.





Cross region geo-redundancy and geo-presence





Second virtual network gateway. This field is the virtual network gateway of the VNet that you want to create a connection to.





Layer 3 connectivity





virtual cross-connections to the Microsoft cloud through the co-location provider’s Ethernet exchange. 





Microsoft uses BGP, 





the peered virtual networks can exist in any Azure public cloud region 





A shared key





this configuration requires two virtual network gateways for the same virtual network, 





without going over Internet-facing endpoints.





Layer 2 cross-connections, or managed Layer 3 cross-connections 





but not in Government cloud regions. 





Azure Traffic Manager and Load Balancer, 





using the gateway type VPN





set up highly available workload with geo-redundancy across multiple Azure regions.





The gateway subnet must be named GatewaySubnet





public IP address of your VPN gateway





other using the gateway type ExpressRoute.





Redundancy





ExpressRoute circuit consists of two connections to two Microsoft Enterprise edge routers (





Regional multi-tier applications with isolation or administrative boundary





ExpressRoute, establish connections to Azure at an ExpressRoute location, such as an Exchange provider facility, or directly connect to Azure 





gateway transit 





peered virtual networks to share the gateway and get access to resources. 





through point-to-point Ethernet links. 





can set up multi-tier applications with multiple virtual networks connected together due to isolation 





traffic between peered virtual networks is private. 





is kept on the Microsoft backbone 





integrate your WAN with the Microsoft cloud. 





Policy-based VPNs





IPVPN providers, 





combine cross-premises connectivity with inter-virtual network connectivity.





Connectivity to Microsoft cloud 





MPLS) VPN, 





Service chaining enables you to direct traffic from one virtual network to a virtual appliance, or virtual network gateway, in a peered virtual ne [...]





enable access to the following services: 





fast and reliable connection to Azure with bandwidths up to 100 Gbps, 





low-latency, high-bandwidth 





Microsoft cloud can be interconnected to your WAN to make it appear just like any other branch office. 





resources in one virtual network to communicate with resources in a different virtual network, 





so ExpressRoute requires Microsoft authorization.





Connectivity to all regions within a geopolitical 





ability to transfer data across Azure subscriptions, 





deployment models, and across Azure regions.





can only be used on the Basic gateway SKU 





No downtime to resources in either virtual network when creating 





can have only 1 tunnel 





Extend and connect your datacenters





can only use Policy-based VPNs for S2S connections, 





Use ExpressRoute to both connect and add compute and storage capacity 





Most VPN Gateway configurations require a Route-based VPN.





existing datacenters. 





can enable the ExpressRoute premium add-on feature to extend connectivity across geopolitical boundaries. 





Route-based VPNs





use routesin the IP forwarding or routing table to direct packets into their corresponding tunnel interfaces. 





Build hybrid applications





build applications that span on-premises infrastructure and Azure without compromising privacy or performance. 





Resources in one virtual network cannot communicate with the IP address of an Azure internal load balancer 





if you have a private data center in California connected to ExpressRoute in Silicon Valley, and another private data center in Texas connected to [...]





peered virtual network. 





load balancer and the resources that communicate with it must be in the same virtual network.





cross-data-center traffic will traverse through Microsoft's network.





ExpressRoute circuits for a wide range of bandwidths from 50 Mbps to 10 Gbps. 





pick a billing model 



# Module 6 Monitoring





Azure Monitor Service

Monitoring - collecting and analyzing data - to determine the performance - health - availability - business application - dependent resources Monitors - Metrics - Logs





Azure Advisor

Advisor Recommendations give best practices Located: Click All services. In the service menu pane, under Monitoring and Management, click Advisor. 





Action Groups

-Several action can be grouped together -Can be reused with other alerts Runbooks -Automation procedures https://docs.microsoft.com/en-us/azure/automation/automation-runbook-types https://docs.microsoft.com/en-us/azure/automation/automation-first-runbook-textual





Managing Alerts

The different states helps us know whats happening in regard to the Alerts





Log Analytics Scenarios

Customers told MS that Monitoring helped them in: - Tracking updates - Change tracking 





Log Analytics Querying

Log Anaylitics - workspace - View Designer - View Dashboard tab





Alerts





Connected Sources are the computers and other resources that generate data collected by Log Analytics. 

Data sources





Data sources are 





Monitor provides 





Azure Activity Log is a subscription log that provides insight into subscription-level events that have occurred in Azure. 





Alerts proactively notify you when important conditions are found in your monitoring data. 





action group is a collection of notification preferences defined by the owner 





default Alerts page 





To get started with Log Analytics you need to add a workspace. 





data collected by Azure Monitor 





can collect data from a variety of sources. 





alert on metrics and logs 





personalized cloud consultant that helps you follow best practices 





provides several event categories. 

add a filter to see these





detail page is displayed when you select an alert. 





provides a query syntax to quickly retrieve and consolidate data in the repository. 





provides a summary of alerts that are created within a particular time window. 





different kinds of data collected 





provides tools to monitor, diagnose, view metrics, 





collecting and analyzing 





you can filter your Activity Log by these fields:





determine if traffic is being directed to the intended destination by showing the next hop. 





information about ingress and egress IP traffic through an NSG. 





diagnose connectivity issues from or to the internet and from or to the on-premises environment. 





two fundamental types, 





can monitor communication between a virtual machine and an endpoint. 





performance, health, and availability of your business application and the resources 





include but are not limited to:





can include events and performance data 





can include agents installed on Windowsand Linuxcomputers that connect directly or agents in a connected System Center Operations Manager manageme [...]





Azure resources helping you understand the health, operation and performance of your system.





Metrics





enables you to change its state.





logs are written in JSON format 





alerts use action groups, 





Windows and Linux agents, 





aspect of a system at a particular point in time. 





named groups of notifications 





Automate remote network monitoring with packet capture.





You create a new alert rule with the following three steps:





operational data to updates on Service Health events.





and 





IIS logs 





actions that can be reused in multiple alerts.





Logs are activity logs, diagnostic logs, and telemetry from monitoring solutions; analytics queries help with troubleshooting and visualizations.





Azure Monitor 





VPN diagnostics can troubleshoot the health of the gateway, or connection, and provide detailed logging. 





collects data from each of the following tiers:





You can set the state of an alert to specify where it is in the resolution process. 





can determine the ‘what, who, and when’ 





Select up to five Azure subscriptions. 





All alert creation 





Logs





different kinds of data organized into records with different sets of properties 





notifying you of critical issues so that you can resolve them before they become problems.





can use Connection Troubleshoot to:





When you configure the Log Analytics 

Log Analytics workspace - Advanced Settings - Data





notify a person by email or SMS the person 

Email, SMS and many other ways to respond to an alert





notify you of critical conditions and potentially take automated corrective actions 





Azure Monitor uses a version of the Data Explorerquery language 

https://docs.microsoft.com/en-us/azure/data-explorer/write-queries https://docs.microsoft.com/en-us/azure/azure-monitor/log-query/log-query-overview https://dataexplorer.azure.com/clusters/help/databases/Samples

Public note added a month ago by Brent Denny





is in one place.





Select a single resource group. 





Only alerts with targets in the selected resource group are included in the view.





Data sources include: Windows Event Logs, Windows Performance Counters, Linux Performance Counters, IIS Logs, Custom Fields, Custom Logs, and Sysl [...]





Through activity logs, you can determine:





Gain insight into your network traffic using flow logs





What operations were taken 





The key attributes of an alert rule are:





Only alerts fired within the selected time window are included in the view. Supported values are the past hour, the past 24 hours, the past 7 days [...]





Previously these were in a separate portal.





collecting, analyzing, and acting on telemetry 





Who 





When 





Alert Rules (





status 





values of other properties that might help you research the operation.





and Fired Alerts (





ITSM

ServiceNow, Provance, Cherwell, and System Center Service Manager.





State





Connection Troubleshoot can also provide a topology (graphical) view from your source to destination, as shown in the following illustration.





Activity logs are kept for 90 days. 





are differentiated, so the operational and configuration views are separated.





Diagnose VPN connectivity issues





example, this query returns a count of the top 10 errors in the Event log during the last day. The results are in descending order.





new alerts authoring experience guides the user along 





If the connection fails, IP flow verify tells you which security rule allowed or denied the communication, 





process of configuring an alert rule, 





Next hop also returns the route table associated with the next hop. 





can pin the filtered state to the dashboard 





makes it simpler to discover the right things to get alerted on.





soon as you create an Azure subscription and start adding resources 





Signals are emitted by the target resource 





download the search results as a CSV 





cloud-based hybrid network monitoring solution that helps you monitor network performance between various points 





Metric, Activity log, Application Insights, and Log.





Runbook

Automation scripts





Azure Monitor starts collecting 





Alert state is set by the user. 





Activity Logs record when resources are created or modified. Metrics tell you how the resource is performing and the resources that it's consuming [...]





in your network infrastructure. 





On the left are the sources of monitoring data that populate these data stores. On the right are the different functions that Azure Monitor perfor [...]





Monitor condition is set by the system. 





common operators 





monitor the performance of Azure ExpressRoute. 





Extend the data you're collecting 





Network performance monitor detects network issues like traffic blackholing, routing errors, and issues that conventional network monitoring metho [...]





In this case, the destination VM is unreachable, and a listing of hops is shown.





by enabling diagnostics and adding an agent to compute resources. 





examples of different supported network troubleshooting scenarios include:





collect telemetry for the internal operation of the resource and allow you to configure different data sources to collect logs and metrics from Wi [...]





Checking the connectivity and latency to a remote endpoint, 





Connectivity between an Azure VM and an Azure resource like Azure SQL 





enables you to generate a visual diagram of the resources in a virtual network, 





Connectivity between VMs in different VNets connected using VNet peering.



# Module 7 Data Protection





Locally-redundant Storage

- 11 9s of Object Durability - Lowest cost for replication Microsoft recommends using either - zone-redundant storage (ZRS) or - geo-redundant storage (GRS)





Zone-redundant Storage

Not in Australia Replicates Data over 3 storage clusters - Storage Clusters are physically seperated Data Centres NOT effective if a regional disater strikes - MS recommends GRS for ultimate protection





Geo-redundant storage

Geo-redundant storage (GRS) is the default - GRS replicates your data to a secondary region - GRS costs more than LRS, - Geo-redundant storage (GRS) is designed to provide at least 99.99999999999999% (16 9's) durability of objects over a given year GRS and RA-GRS - First Replcates the data in a LRS - Then replicates the data to another Region and in a LRS of that region also GRS - Can perform an account failover the the other region - Failover may lose data if the Geo-Replication has not happened (Possible up to 15 min.) - RA-GRS allows you to read from the other region even without a failover





Geo-zone-redundant Storage





Azure Backup

Perform In-Cloud and On-Prem backups to the Cloud - No charge for data transferred (backup and restore) - Short and long term retension - Storage options LRS and GRS





MARS Agent

Backup agent will only work on MS OS's No Linux support 





Azure Site Recovery Scenarios

Creating an automatic DR site in the cloud - Supports MS - Linux - HyperV - VMware - Copies Data - Constantly monitors protected instances from the cloud Includes management of replication and fail-over





Virtual Machine Data Protection

Multiple options - Azure Backup - Azure Site Recovery - Managed Disk Snapshots - point in time capture of a single disk state - Images - This is all the disks that were associated with a VM - syspreped 





Workload Protection Needs

Enable backup for individual Azure VMs. - Azure Backup installs an extension to the Azure VM agent that's running on the VM. The agent backs up the entire VM. Run the MARS agent on an Azure VM. - This is useful if you want to back up individual files and folders on the VM. Back up an Azure VM to a System Center Data Protection Manager (DPM) - Then backup the DPM/MABS (Microsoft Azure Backup Server) to a vault There are other backup solutions in the Azure Marketplace as well





Recovery Services Vault VM Backup Options

Recovery Services vault is a storage entity in Azure that stores data. The data is typically copies of - data - or configuration information for virtual machines (VMs), Backup Azure virtual machines. Backup on-premises virtual machines including: - Hyper-V - VmWare - System State - Bare Metal Recovery





Azure Backup Server

Backing up to MABS/DPM provides app-aware backups optimized for common apps such as SQL Server, Exchange, and SharePoint On-premises machines, don't need to install the MARS agent on each machine you want to back up. - Each machine runs the DPM/MABS protection agent You have more flexibility and granular scheduling options You can manage backups for multiple machines that you gather into protection groups in a single console.





On-Premises File and Folder Backups

Create the recovery services vault. Download the agent and credential file. Install and register agent. Configure the backup.





Once your virtual machine snapshots are safely in the recovery services vault it is easy to recover them.





When you enable replication for an Azure VM, the following happens:





data 





methods for backing up virtual machines.





Recovery Services vault





Azure-based service you can use to back up (or protect) and restore your data in the Microsoft cloud. 





three copies of your 





six copies of your data.





Microsoft Azure Recovery Services (





always replicated to ensure durability and high availability. 





Enable backup for individual Azure VMs. 





storage entity in Azure that houses data. 





easy and follows a simple process.





There are several backup options available for VMs, 





replicated three times across two to three facilities, either within a single region or across two regions.





three times within the primary region and is also replicated three times in a secondary region 





Mobility service extension is automatically installed on the VM. 





installed on the Window 





typically copies of data, 





This method can be used for specialized workloads, virtual machines, or files, folders, and volumes. Specialized workloads can include SharePoint, [...]





replaces your existing on-premises or off-site backup solution with a cloud-based 





configuration information for virtual machines (VMs), workloads, servers, or workstations. 





backing up Azure VMs running production workloads, 





Continuous replication begins for the VM. 





supports application-consistent backups for both Windows and Linux VMs. 





writes are immediately transferred to the cache storage account 





Run the MARS agent on an Azure VM. 





hold backup data for various Azure services such as IaaS VMs (Linux or Windows) 





six copies of your data.





storage cluster is physically separated from the others and resides in its own availability zone. 





Data is replicated to a secondary geographic location and provides read access 





combines the high availability of zone-redundant storage with protection from regional outages as provided by geo-redundant storage





creates recovery points that are stored in geo-redundant recovery vaults. 





Site Recovery processes the data in the cache, and sends it to the target storage account, 





file, folder, and volume-level restore only.





Back up an Azure VM to a System Center Data Protection Manager (DPM) 





No support for Linux.





or to the replica managed disks.





restore the whole VM or just specific files. 





Recovery Services vaults make it easy to organize your backup data, while minimizing management overhead.





provides app-aware backups 

Application-aware backups capture the state of application data at the time of the backup, including data in memory and pending transactions





After the data is processed, 





recovery points are generated every five minutes. 





Then back up the DPM server/MABS to a vault using Azure Backup.





protects your VMs from a major disaster 





The 





on-premises machines, 





When you initiate a failover, 





benefits





Offload on-premises backup





VMs are created in the target resource group, target virtual network, target subnet, and in the target availability set. During a failover, you ca [...]





Each machine runs the DPM/MABS protection agent, 





ZRS is not yet available in all regions.





LRS)





three copies of your data.





you can recover your application with a single click in matter of minutes. You can replicate to an Azure region of your choice.





Changing to ZRS 





flexibility and granular scheduling 





requires the physical data movement 





Back up Azure IaaS VMs





LRS provides at least 99.999999999% (11 nines) durability





manage backups for multiple machines that you gather into protection groups 





ZRS may not protect your data against a regional disaster 





development and test environments, snapshots provide a quick and simple option for backing 





particularly useful when apps are tiered over multiple machines 





VMs that use Managed Disks. 





16 9's) durability 





Extending on-premises data protection solutions into Azure. 





snapshot is a read-only full copy of a managed disk 





Backup steps





Get unlimited data transfer

Free





data is still accessible for both read and write operations 





does not limit the amount of inbound or outbound data you transfer, or charge for the data that is transferred. 





backup solutions available today in the Azure Marketplace.





snapshots exist independent of the source disk 





can be used to create new managed disks. 





LRS is the lowest-cost replication option





data size of 10 GiB, that snapshot is billed only for the used data size of 10 GiB.





Keep data secure





secure transmission 





Managed disks also support creating a managed custom image. 





can create an image from your custom VHD in a storage account or directly from a generalized (sysprepped) VM. 





Get app-consistent backups





contains all managed disks associated with a VM, 





application-consistent backup means a recovery point has all required data to restore the backup copy. 





custom image enables creating hundreds of VMs using your custom image 





Retain short and long-term data





primary region becomes unavailable, you can perform an account failover (preview) to the secondary region. When 





snapshot is a copy of a disk at the point in time the snapshot is taken. 





Automatic storage management





changes that haven't yet been geo-replicated may be lost. 





number of minutes of potential data that's lost is known as the RPO. 





snapshot doesn't have awareness of any disk except the one it contains. 





Multiple storage options





measure of how long it takes to perform the failover and get the storage account back online. 





Locally redundant storage (





Geo-redundant storage (



# Module 8 Network Traffic Management





System Routes

These are Automatic Azure managed routes that route traffic: - Within a subnet - Between subnets in a Virtual Network - VMs to the Internet - between VMs through a Vnet-VNet VPN - Site to Site and Express route through VPN gateway 





User Defined Routes

You may want certain subnet traffic to be directed to a virtual appliance. - You might place an appliance between subnets or a subnet and the internet. - Create your own route to direct traffic to the correct next hop





Create a Routing Table

Key notes here are to" - Allow BGP propagation - Routing traffic to a Virtual Appliance like a Firewall with IP fowarding





Associate 





Azure Load Balancer

Layer 4 Load balancer - HA and load balancing - uses health probes Backend Pool - Availability Set or Scale Set





Public Load Balancer

Public LB maps Public IP and port to an Private IP and Port for inbound and subsequent return traffic 





Internal Load Balancer

Within a virtual network. - Load balancing from VMs in the virtual network to a set of VMs that reside within the same virtual network. For a cross-premises virtual network. - Load balancing from on-premises computers to a set of VMs that reside within a virtual network. For multi-tier applications. - Load balancing for internet-facing multi-tier applications where the back end tiers are not internet-facing. For line-of-business applications. - Load balancing LOB Apps hosted in Azure - without additional load balancer hardware or software. - This includes on-premises servers that are in the set of computers whose traffic is load-balanced.





Load Balancer SKUs

- Cannot change SKU after creation - A resource can only refernce one SKU - LB Rules cannot span two virtual networks - No cost for basic LB - Standard LB has a cost / rule - LB front ends are not available across Global Network Peering





Backend Pools

Basic LB Pool - VM - Availability Set VMs - VM scale set Standard LB Pool - An availabilty set - VM scale set





Load Balancer Rules

Can create an inbound NAT rule to (port forward) - port forward traffic from a specific port of a specific frontend IP address - to a specific port of a specific backend instance inside the virtual network. 





Session Persistence





Health Probes

Two main ways to configure health probes: HTTP and TCP - HTTP - looking to receive a 200 OK response - TCP - looking for a successful 3-way handshake There is also a Guest Agent probe - Only use this when TCP and HTTP are not possible





Azure Traffic Manager

This is a GSLB like service - Intelligent DNS load balancing





Traffic Manager Features

- LB of resources - Automatic failover - Proximity LB - Upgrades without Outage - On prem and In-Cloud resource LB - Support for large complex deployments





Performance Routing

Traffic Manager maintains an Internet Latency Table to track the round-trip time between IP address ranges and each Azure datacenter Looks up the source IP address of the incoming DNS request in the Internet Latency Table - Traffic Manager chooses an available endpoint in the Azure datacenter that has the lowest latency for that IP address range, - then returns that endpoint in the DNS response





Geographic Routing

Knowing a user’s geographic region and routing them based on that is very important. - Complying with data sovereignty mandates Manual setup of - Geographic Locations database to endpoints





Weighted Routing

Need LB but - want to prefer an endpoint over others - Lowest number has the highest priority





Implementing Traffic Manager Profiles

Must create a profile. The profile will include - the routing method - DNS time to live (TTL)





An internal load balancer directs traffic only to resources that are inside a virtual network or that use a VPN 





Traffic Manager profile must also define the endpoints. 





back-end address pool contains the IP addresses 





Azure automatically handles all network traffic routing. 





reliability for its services by deploying one or more backup services in case their primary service goes down.





to associate the Public subnet with the new routing table. 





define how traffic is distributed to the backend pool. 





must provide Name, Subscription, Resource Group, Location





what if you want to do something different? 





that are connected to the load balancer.





10.0.1.0/24.

Destination





maps the public IP address and port number of incoming traffic to the private IP address and port number of the VM, 





following situations are managed by these system routes:





rule maps a given frontend IP and port 





source IP, source port, destination IP, destination port, and protocol type) hash to 





Azure endpoints





Frontend IP addresses and virtual networks are never directly exposed to an internet endpoint. 





Virtual network gateway route propagation

When you exchange routes with Azure using BGP, - routes are not added to the route table of all subnets when Route propagation is disabled. - Disabled on the subnet-routetable property Normally you would want the propagation of routes





set of backend IP addresses and port combination. 





routing, firewalling, or WAN optimization. 





Standard SKU





rule the frontend, backend, and health probe information should already be configured. 





Basic SKU





Backend pool endpoints





want certain subnet traffic to be directed to this virtual appliance. 





Standard Load Balancer is the newer Load Balancer product with an expanded and more granular feature 





External endpoints





You want to ensure all traffic from the Public subnet goes through the NVA to the Private subnet.





10.0.2.4.

Routed through this subnet





set 





probes: HTTPand TCP.





you can configure user-defined routes (UDRs). 





Communication between the subnets and from the frontend to the internet are all managed by Azure using the default system routes.





internal load balancer enables the following types of load balancing:





every 15 seconds, by default). 





routing traffic to the location that is closest to the user. 





defining routes that specify the next hop of the traffic flow. 





may not change the SKU of an existing resource.





HTTP 200 within the timeout period (default of 31 seconds). 





Standard SKU you can have up to 1000 instances 





resource can reference one SKU, 





Each route table can be associated to multiple subnets, 





Load Balancer rule cannot span two virtual networks. 





subnet can only be associated to a single route table. There 





Basic SKU you can have up to 100 instances.





NAT rule is explicitly attached to a VM (





must be in the same virtual network.





no additional charges 





no charge for the Basic load balancer. 





Load Balancing rule need not be.





Packets are matched to routes using the destination. 





Standard load balancer is charged based on number of rules and data processed.





destination can be an IP address, a virtual network gateway, a virtual appliance, or the internet. 





establishing a successful TCP session 





frontends are not accessible across global virtual network peering.





guest agent probe. This probe uses the guest agent inside the VM. 



# Module 9 Azure Active Directory





Azure Active Directory Editions

P2 - Azure Active Directory Identity Protection is more than a monitoring and reporting tool. To protect your organization's identities, you can - configure risk-based policies that automatically respond to detected issues when a specified risk level has been reached These policies, in addition to other Conditional Access controls provided by Azure Active Directory and Enterprise Mobility + Security (EMS), can either - automatically block or - initiate adaptive remediation actions including password resets and multi-factor authentication enforcement.





Azure AD Directories (Tenants)

Multiple Tennants: - For example: You could have a tenant for Office 365, another tenant a for testing environment - Administrative Independence - Sync Independence





Azure AD Connect Health

Monitor and gain insights into - AD FS servers, - Azure AD Connect, - AD domain controllers. Monitor and gain insights into - synchronizations that occur between your on-premises AD DS and Azure AD. Monitor and gain insights into your - on-premises identity infrastructure that is used to access Office 365 or other Azure AD applications





Device Management

To get a device under the control of Azure AD either Register device to Azure AD - Enables you to manage a device’s identity - Provides the device with an identity that is used to authenticate the device when a user signs-in to Azure AD. - You can use the identity to enable or disable a device. Joining a device - Is an extension to registering a device. - It also changes the local state of a device. - Changing the local state enables your users to sign-in to a device using an organizational work or school account instead of a personal account. Registration + Intune - Provides additional attributes - Allows creation of conditional access which enhances security





Azure AD Joined Devices

Great video https://www.youtube.com/watch?v=NN14TVisuSU 





Hybrid AD Joined Devices

devices that are joined both to your on-premises Active Directory and your Azure Active Directory - IT departments to manage work-owned devices from a central location. - Users to sign in to their devices with their Active Directory work or school accounts.





tenant 





environment has an on-premises AD 





integrate your on-premises directories with Azure Active Directory. 





dedicated instance of an Azure AD 





Single sign-on 





AD DS is the traditional deployment of Windows Server-based Active Directory 





to any cloud or on-premises web app.





also want to benefit from the capabilities provided by Azure Active Directory, 





created whenever you sign up for a Microsoft cloud service, such 





AD Join has these benefits.





as Office 365 or Azure. 





implement hybrid Azure AD joined devices. 





fine-tune the process of registering and joining devices 





challenge of ensuring that this environment is healthy so that users can reliably access resources both on premises and in the cloud from any devi [...]





configuring the device settings.





tenant is not the same as a subscription. 





joined both to your on-premises Active Directory and your Azure Active Directory.





Password writebackis a feature enabled with Azure AD Connect that allows password changes in the cloud to be written back to an existing on-premis [...]





single sign-on (SSO) access to thousands of cloud SaaS Applications like Office365, Salesforce, DropBox, and Concur.





following features:





Users may join devices to Azure AD





can choose cloud authentication 





When users sign-in using Azure AD, Pass-through authentication validates the users’ passwords directly against an organizations on-premise Active [...]





Works with iOS, Mac OS X, Android, and Windows devices.





subscription is typically tied to a credit card 





Azure AD password hash synchronization and Azure AD Pass-through Authentication. You can also choose federated authentication 





multiple on-premises Active Directory forests. 





To get a device under the control of Azure AD, you have two options:





allows:





a tenant is an instance of Active Directory. 





manage work-owned devices from a central location.





Premium P1 and P2 online.





Feature benefits





result of a merger or acquisition. 





synchronize user passwords from an on-premises Active Directory instance to a cloud-based Azure AD instance. 





sign in to their devices with their Active Directory work or school accounts.





Registering





enables you to 





all forests must be reachable by a singleAzure AD Connect sync server. 





manage a device’s identity. 





Additional local administrators on Azure AD joined devices





registration provides the device with an identity that is used to authenticate the device when a user signs-in to Azure AD. 





select the users that are granted local administrator rights on a device. 





Protect on-premises web applications with secure remote access.





full suite of identity management capabilities 





multi-factor authentication, 





You sign in to the service by using the same password you use to sign in to your on-premises Active Directory 





device registration, 





You could have a tenant for Office 365, 





self-service password management, 





self-service group management, privileged account management, role-based access control, application usage monitoring, rich auditing and security [...]





tenant a for testing environment, 





supports installing a second server in staging 





provides AD FS management capabilities such as certificate renewal and additional AD FS server deployments.





Joining





tenant for Microsoft Intune. 





server in this mode reads data from all connected directories but does not write anything to connected directories. 





This means, it provides you with all the benefits of registering a device and in addition to this, it also changes the local state of a device. Ch [...]





Easily extend Active Directory to the cloud.





Users may register their devices with Azure AD





Azure AD can be integrated with an existing Windows Server Active Directory, 





password synchronization component takes the user’s password hash from on-premises Active Directory, encrypts it, and passes it as a string to Azu [...]





Here are some characteristics of Azure AD that make it different.





disaster where the primary server fails, you can fail over to the staging server. 





Protect sensitive data and applications.





create or delete a resource in one tenant, it has no impact on any resource in another tenant, 





✔️ Registration combined with a mobile device management (MDM) solution such as Microsoft Intune, provides additional device attributes in Azure A [...]





you are an Office365, Azure or Dynamics CRM Online customer, you might not realize that you are already using Azure AD. 





use one of your domain names with one tenant, it cannot be used with any other tenant.





cannot be queried through LDAP. 





Reduce costs and enhance security with self-service capabilities.





non-administrative user of tenant ‘Contoso’ creates a test tenant 'Test,





This feature can be configured without using a federation service so that any organization, 





Require Multi-Factor Auth to join devices





not use Kerberos 





regardless of size, can implement a hybrid identity solution. 





user who creates a tenant is added as an external user in that new tenant and assigned the global administrator role in that tenant.





includes federation services, 





administrators of tenant ‘Contoso’ have no direct administrative privileges to tenant 'Test,' unless an administrator of ‘Test’ specifically grant [...]





Having multiple Azure AD Connect sync servers connected to the same Azure AD tenant is not supported, 





✔️ It is important to understand that this is same sign-in, not single sign-on. The user still authenticates against two separate directory servic [...]





Synchronization independence.





no Organizational Units (





Maximum number of devices





Users may sync settings and app data across devices



# Module 10 Securing Identities





Enabling MFA

Choose which users will use MFA from the MFA option - Users need to be licenced for Microsoft Online Services to be able to use MFA Azure MFA is included free of charge for global administrator security. 





Requiring MFA

Conditional access - enforce controls on the access to apps - based on specific conditions from a central location. Conditional access comes with six conditions: - user/group, - cloud application, - device state, - location (IP range), - client application - sign-in risk. With access controls, - you can either Block Access altogether - Grant Access with additional requirements: - Require MFA from Azure AD or an on-premises MFA (combined with AD FS). - Grant access to only trusted devices. - Require a domain-joined device. - Require mobile devices to use Intune app protection policies.





One-time Bypass

Skip MFA - Authenticate a single time without performing two-step verification - This is temporary and expires after the time specified (sec)





Fraud Alerts

Configure the fraud alert feature so that your users can report fraudulent attempts to access their resources - User reports fraud, their account is blocked for 90 days - or until an administrator unblocks their account - User normally types # to verify the Two stage auth - To report Fraud - user types # - can customise the code - Default code = 0 - 0# reports fraud





Azure AD Identity Protection

Azure AD Identity Protection is available to - Enterprise Mobility Suite and/or the - Azure AD Premium P2 service. Azure AD Identity Protection enables you to: - Detect potential vulnerabilities affecting your organization’s identities - Configure automated responses to detected suspicious actions that are related to your organization’s identities - Investigate suspicious incidents and take appropriate action to resolve them - Identity Protection capabilities Uses Machine learning algorithms and heuristics to detect suspicious actions related to your user's identities. - The system creates a record for each detected suspicious action. (risk events). Azure AD Identity Protection lets you set risk-based Conditional Access policies to automatically protect your users





Azure AD Risk Events

Azure Active Directory detects six types of risk events: - Leaked credentials - Sign-ins from anonymous IP addresses - using an anonymous proys - Impossible travel to atypical locations - Logins happening from different locations too quickly - Sign-in from unfamiliar locations - Machine learning 





User Risk Policy

Each login is checked for compromising behaviour - Each event recorded can be dealt with manually - You can create policies to allocate risk levels to events Risk events can be detected: - Instantly for some behaviours - After some time for other behaviours Policies can: - Block access - Allow access - Allow access but require an immediate password change





Sign-in Risk Policy

Azure AD detects the probability that a user account has been compromised. Configure Policy - Users and groups the policy applies to - Assign the condition (Low and above, Medium and above, or High) - The access type you will enforce for the user based on sign-in risk level - Set Enforce Policy to On - You can configure a sign-in risk security policy to require MFA:





Security Best Practices





Self-Service Password Reset

Time and money wasted - help desk resetting passwords SSPR - Decide who you allow to do this





Comparing SSPR to MFA

Azure AD self-service password reset (SSPR) and MFA may ask for additional information, - known as authentication methods or security info Administrators can define in policy which - authentication methods are available - to users of SSPR and MFA.





To enable MFA, go to the User Properties in Azure Active Directory, 





Trusted IPs is a feature to allow federated users or IP address ranges to bypass two-step authentication. 





Configure the fraud alert 





If you want your users to register for password reset, you can require that they register when they sign in through Azure AD. 





Azure Multi-Factor Authentication (MFA) helps safeguard access to data and applications while maintaining simplicity for users. 





Azure AD analyzes each user-sign 





Azure AD self-service password reset (SSPR) and MFA may ask for additional information, known as authentication methods 





Azure AD detects the probability that a user account has been compromised. 





authenticate a single time without performing two-step verification. The bypass is temporary and expires after a specified number of seconds.





users can report fraudulent attempts to access their resources. 





evidence of a compromised account or any suspicious activity, 





you pick the number of authentication methods required to reset a password 





malicious users use credential theft 





then the Multi-Factor Authentication option. 





select the users that you want to modify and enable for MFA. 





by using the mobile app or through their phone. 





For risk events that the system detects, 





adaptive machine learning algorithms and heuristics to detect suspicious actions 





resolve those events manually, 





Administrators can define in policy which authentication methods are available 





user reports fraud, their account is blocked for 90 days or until an administrator unblocks their account. 





Azure AD detects risk event types in real-time and offline. 





For organizations 





configure conditional access policies that apply to a specific user risk level 





derived from consensus opinion and Azure platform capabilities and feature sets.





first determine who will be enabled to use self-service password reset. 





need to be compliant 





On first-time sign-in, 





You can choose from email notification, a text or code sent to user’s mobile or office phone, or a set of security questions.





PCI DSS 





users are prompted to configure their MFA settings. 





contributes to a risky sign-in.





these credentials can be extracted in the form of hashes, tickets, or even plaintext passwords. 





system can detect some risk events in real-time 





security questions, 





can be configured to require a certain number of questions 





other risk events require more time to analyze pattern and behavior, 





report fraud during initial greeting: 





Authentication Method





Selectedoption is useful for creating specific groups who have self-service password reset enabled. 





users receive a phone call to perform two-step verification, they normally press # to confirm their sign-in. To report fraud, the user enters a co [...]





MFA two-step verification 





risk event type identifies IP addresses from which a high number of failed sign-in attempts were seen, across multiple user accounts, over a short [...]





such 





as 





analyzes each user sign-in with the intention of detecting suspicious actions, 





impossible travel to atypical locations. 





Azure MFA is included free of charge 





matches traffic patterns of IP addresses used by attackers, 





Azure AD Identity Protection is a service that helps to ward off compromised user accounts and configuration vulnerabilities. 





global administrator security. 





know (typically a password)





accounts are either already or are about to be compromised.





have (a trusted device 





Azure AD calculates a value representing the probability (low, medium, high) that the sign is not performed by the legitimate user. 





Leaked credentials





are (biometrics)





service is available from Azure Marketplace 





more security with less complexity





set up by an organization's global administrator. 





you can only enable MFA for organizational accounts stored in Active Directory. 





When the system detects a risk event 





available to subscribers to Microsoft's Enterprise Mobility Suite and/or the Azure AD Premium P2 service.





that hasn't been resolved 





considered an active risk event. 





Detect potential vulnerabilities affecting your organization’s identities





Configure automated responses to detected suspicious actions 





Mitigate threats with real-time monitoring and alerts





Investigate suspicious incidents and take appropriate action to resolve them





security monitoring and machine-learning-based reports that identify inconsistent sign-in patterns. 





Sign-ins from anonymous IP addresses





risk policy lets you block access access to resources or require a password change 





analyses your configuration and detects vulnerabilities 





Deploy on-premises or on Azure





uses adaptive machine learning algorithms and heuristics to detect suspicious actions 





Configure the user risk policy





Impossible travel to atypical locations





lets you set risk-based Conditional Access policies to automatically protect your users. 





Use with Office 365, Salesforce, and more





Add protection for Azure administrator accounts





Sign-in from unfamiliar locations





Sign-ins from infected devices



# Module 11 Governance and Compliance





Management Groups

Management Groups are like compliance containers for subscriptions - Mgmt Groups can contain other Mgmt Groups forming a hierarchy - Assign governance conditions to the mgmt groups - Subscriptions under the MG will inherit the conditions - Example - Create VMs in a set region ONLY 





Creating Management Groups

Can create mgmt groups - Portal - PowerShell - CLI Cannot use - Templates ( at this time ) Mgmt Group Creation - MG ID - Cannot be altered after making the group - internally referenced - Display Name - Name shown in the portal





Check Resource Limits

Subscriptions - Usage and Quotas Track Resources againts Limits - You can request an increase in the limits - unless they are at the maximum allowed





Resource Tags

Makes it easy to categorise resourses - you can retrieve resources from - different resource groups - that relate to the same category Downloading usage stats as CSV the tags are included - this could make it easy to create DB/SpreadSheet reports grouping usage by TAG





Billing

Billing calculator - Gives estimates of costs Billing Alerts - help you monitor and manage billing activity for your Azure accounts. - You can set up a total of five billing alerts per subscription, with a different threshold - Up to two email recipients for each alert. - Monthly budgets are evaluated against spending every four hours.





RBAC Concepts

Configured by selecting - a role (the definition of what actions are allowed and/or denied), - associating the role with a user, group or service principal. - Finally, user+role is scoped to either the - entire subscription - a resource group - specific resources





RBAC Roles

Over 100 Predefined roles Common Roles: - Owner - Contributor - Reader Look for the IAM blade in a resource





Administrator Permissions

Azure AD - P1 or P2 premium accounts are required to create custom Roles - From Azure AD - "Roles and Administrators" blade - can view associated roles





Role Assignment

Roles can also be scoped to - Subscription - resource groups - individual resources. Roles can be paired with - User - Group - Service Principals Service Principals - Example An app may need access to an Azure Service - A Service Principal is created based on the App definition





Role Definitions

Each role is a JSON file. It includes: - Name - ID - Description. It also includes - allowable permissions (Actions), - denied permissions (NotActions), - scope 





User Accounts

To gain access to Resources users need an account User Account source: - Cloud identities - Users that only exist in Azure AD. - Directory-synchronized identities - Users brought in to Azure through Azure AD Connect. (On prem originally) - Guest users - Users from outside Azure. (like Google or Microsoft accounts).





Adding User Accounts

Portal PowerShell CLI - az ad user create





Bulk User Accounts

Use CSV and PowerShell - Pipe by PropertyName - Get the CSV headers right (Spelling)





Group Accounts

Group helps organize users to make it easier to manage permissions - Security - Distribution Membership - Directly Assigned - Manual assignment - Dynamic Assigned - Based on attribute policy rules (i.e. if part of the Sales "Department" then Dynamically added to some groups)





Adding Group Members

Portal PowerShell CLI 





Adding a Group Owner

Group owners - manage a group and its members





Azure Policy

Azure Policy - enforce different policys for resources so they comply with security standards Examples: - Locations allowed - Certificate expiry alerts - Standard Tags are applied Types: - Logging - Apply to Management Group - Remediation History of Changes to resources by Remediation Policies - What has been added - What has been removed





Implementing Azure Policy

Browse Policy Definitions. - A Policy Definition expresses what to evaluate and what actions to take. Create Initiative Definitions. - An initiative definition is a set of Policy Definitions to help track your compliance state for a larger goal. For example, ensuring a branch office is compliant. Scope the Initiative Definition. - You can limit the scope of the Initiative Definition to Management Groups, Subscriptions, or Resource Groups. View Policy Evaluation results. - Once an Initiative Definition is assigned, you can evaluate the state of compliance for all your resources. 





Policy Definitions

Default policies in Azure Import Policy JSON files from GitHub The JSON format is a little different to the standard JSON files (Logic etc. is included) 





Create Initiative Definitions





Scope the Initiative Definition





Pricing Calculator





Managing access to resources 





Access does not need to be granted to the entire subscription. 





role is a set of properties defined in a JSON file. This role definition includes Name, Id, and Description. It also includes the allowable permis [...]





multiple ways to add cloud identities 





ways to get an Azure subscription: 





collection of actions that can be performed 





users who require access to resources must have a user account. 





service in Azure that you use to create, assign and manage policies. 





can use PowerShell to import data into your directory, 





Compliance blade to review non-compliant initiatives, non-compliant policies, and non-compliant resources.





Azure Portal





Initiative Definition. This definition will include one or more policies. 





commonly used subscriptions are:





Group owners are assigned to manage a group and its members by a resource owner (





Billing for Azure services is done on a per-subscription basis. 





Billing Alertshelp you monitor and manage billing activity for your Azure accounts. 





policies enforce different rules over your resources, 





scope determines what resources or grouping of resources the policy assignment gets enforced on.





name and a value. 





Azure management groups provide a level of scope above subscriptions. 





When a 





condition is evaluated against your existing resources and found true, then those resources are marked as non-compliant 





to grant appropriate access to Azure AD users, groups, and services. 





CSV) 





Group owners aren't required to be members of the group. 





Azure Policy does this by running evaluations of your resources and scanning for those not compliant 





Azure PowerShell





user, group, or service is granted access to only a resource group within a subscription, 





Three of the most common roles 





Subscriptions 





help you control how resource usage is reported, billed, and paid for. 





three roles related to Azure accounts and subscriptions:





Policy evaluation happens about once an hour, 





If you need to increase a default limit, there is a Request Increase link. 





Permissions (top).

This is in preview and does not seem to work - Use the powershell instead - as below in demo





All subscriptions within a management group automatically inherit the conditions applied to the management group. 





Reservationshelps you save money 





Users that only exist in Azure AD. 





pre-paying for 





one-year or three-years 





Real time policy evaluation and enforcement. Periodic and on-demand compliance evaluation.





This role has full control over the subscription and is the account that is responsible for billing.





Adding Members to Groups





If your current limit is already at the maximum number, the limit can't be increased.





Users brought in to Azure through a synchronization 





Apply policies to a Management Group with control across your entire organization. 





Directly Assigned





Subscriptions have accounts. 





account is simply an identity in Azure Active Directory (Azure AD) 





Dynamically Assigned





resource or resource group 





Users from outside Azure. 





Real time remediation, and remediation on existing resources.





create rules to enable attribute-based dynamic memberships for groups 





maximum of 15 tag name/value pairs.





Google and Microsoft accounts.





This role has control over all the services in the subscription.





Tags applied to the resource group 





Scope your role





not inherited 





Actions and NotActions properties is not enough to fully implement a role. 





Budgetshelp you plan for and drive organizational accountability. 





Same as Service Administrator but can’t change the association of subscriptions 





must also properly scope your role.





to 





Azure directories.





Every Azure subscription is associated with an Azure Active Directory. 





Account Administrator 





only person with access to the Account Center. 





Typically to grant a user access to your Azure resources, you would add them to the Azure AD directory associated with your subscription. 





Service Administrator 





Service Administrator has management access to cloud resources using the Azure Management Portal, as well as tools like Visual Studio, other SDKs, [...]





Service principals





Service identities are represented as service principals in the 





directory. 





authenticate with Azure AD and securely communicate with one another. 





Additionally, Co-Administrators 





can’t delete the Service Administrator 





assigning roles through the Azure module for Windows PowerShell 





Account Administrators using a Microsoft account must log in every 2 years (





keep the account active. 



# Module 12 Data Services





How CDN Works

- User requests content - edge server fetches content and TTL for file from another source - edge server caches content





CDN Endpoints

 To access cached content on the CDN - use the CDN URL provided in the portal (ASHStorage.azureedge.net//)





CDN Time-to-Live

Content from Blob storage will exist in the CDN cache: - directed by the Cache Control in HTTP header - Global Cache timeout - Custom Cache timeout (matches paths - timeouts)





CDN Compression

Two ways to do CDN Compression: - Compress from Source - CDN just passes the compressed file on - CDN Compression - The CDN created the compressed content





Azure File Sync

Many ways to use File Sync: - Lift and Shift - Branch Office - Backup and DR - File Archiving File Archiving - Frequently Used data stays local - Other files are moved to Cloud Tier - pointer locally points to the URL of a Cloud Tier file





File Sync Components

Sync service Sync group - defines topology for endpooints Registered Server - Azure sync agent Cloud Endpoint Server Endpoint 





File Sync - Initial Steps

Step to setting up the registered server





File Sync - Synchronization

Two more things: Create sync group - Cloud endpoint - Server endpoint 





Import and Export Service

Securely import large amounts of data to: - Azure Blob storage - Azure Files By shipping disk drives to an Azure datacenter.





Components and Requirements

Must prepare disk to hold data securely Need to create an Azure Import Job





Import and Export Tool

This tools prepairs disks and stores data Jounal file is created - state of copy (so that interupted copies can be resumed) WAImportExport.exe has parameters: - PrepImport - /J: JournalFile - /id: SessionID - /Dataset dataset.csv





Import Jobs

When setting up the job in the Azure Portal you will need the: - Journal File





Export Jobs

Transfer data from Azure storage to - hard disk drives - ship to your on-premise sites.





AzCopy

Command line copy tool - Download lastest copy of azCopy Command azCopy /Source: source /Dest: https://<Azure SMB file share> /DestKey: /s /s means recursion





Online - Data Box Gateway

On Prem VM that - You write data to - It transfers data to Azure





Online - Data Box Edge

Physical appliance to perform a similar task to Data Box Gateway - 12 TB max





A CDN profile is a collection of CDN endpoints with the same pricing tier and provider (origin). 





distributed network of servers that can efficiently deliver content to users. 





Several pricing tiers are available. 
