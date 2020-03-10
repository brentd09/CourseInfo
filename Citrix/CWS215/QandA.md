# Questions and answers

## Date : 11 Nov 2019

Question  | Answer
---|---
Method to auto renew our Citrix certifications by attending an authorised course? | From Citrix, "The automatic re-certification should happen in a few weeks after the course, if this does not happen, then submit a support ticket through [training.citrix.com](https://training.citrix.com) informing Citrix of the issue and they will  sort it out."
On prem Citrix with Windows 10 issues regarding working with OneDrive for business | Most Citrix blogs point to - [FsLogix Office 365 Container](https://fslogix.com/products/office-365-container) solution. <BR>Another solution may be [ZeeDrive](http://www.thinkscape.com/Map-Network-Drives-To-Office-365-OneDrive/) It has specific support for Citrix environments. [Another link that might help](https://www.citrix.com/content/dam/citrix/en_us/documents/products-solutions/deployment-guide-office-365-for-xenapp-and-xendesktop.pdf) and yet [another](https://docs.microsoft.com/en-us/DeployOffice/overview-of-shared-computer-activation-for-office-365-proplus?redirectSourcePath=%252fen-us%252farticle%252f836f882c-8ff6-4f19-8b24-0212e0111c94)
Upgrading Citrix License server 7.15 CU3 to CU4 shows the license server component upgraded but the XD component still on CU3 | Citrix employees and Master CCIs have said that they remove the existing Licence server and install the new version as fresh install.
Can WEM be used from Citrix Cloud | YES, check out the docs for it, [WEM service](https://docs.citrix.com/en-us/workspace-environment-management/service.html)

## Date : 12 Nov 2019

Question  | Answer
---|---
PVS created issues with activation of Office and Windows via KMS | [Here](https://support.citrix.com/article/CTX128276) is a Citrix Support article regarding this. 
Local Host Cache is supported with Citrix cloud ONLY if there is an on-prem StoreFront server present| This issue is outlined in [the local host cache](https://docs.citrix.com/en-us/citrix-virtual-apps-desktops-service/manage-deployment/local-host-cache.html) Citrix doc file
What has the recommended external beacon address changed to? | The external beacon should now be  [ping.citrix.com](https://support.citrix.com/article/CTX261993)

## Date : 13 Nov 2019

Question  | Answer
---|---
Is there a way to export and import Citrix policies | If you are exporting and importing policies from and to the same site then [this article](https://support.citrix.com/article/CTX136646) may help. This method can only export Studio policies and there is no way of choosing which policy to export, it's all or nothing through this method. <BR>[This support article may be better](https://support.citrix.com/article/CTX140039) if you need to import policies to GPO from Local Studio policies
  
## Date : 14 Nov 2019

Question  | Answer
---|---
Differences between the installed HDX client and The HTML5 client | Look at this [feature matrix](https://www.citrix.com/content/dam/citrix/en_us/documents/data-sheet/citrix-workspace-app-feature-matrix.pdf) of all the Citrix Clients and features
  
## Date : 15 Nov 2019

Question  | Answer
---|---
What is CIS |   go [here](https://cis.citrix.com/AutoSupport/howitworks/) for an explanation regarding how CIS works
Is there a tool that can check the proxy support for Citrix Cloud | Look [here](https://support.citrix.com/article/CTX260337) for a tool from Citrix that will help in this regard.

## Date : 10 Mar 2020

Question  | Answer
---|---
Published Content how it works in XD7 |  [Publishing Content and how it is used](https://docs.citrix.com/en-us/xenapp-and-xendesktop/7-15-ltsr/install-configure/publish-content.html)
Queue for deletion of Difference disks - can this be modified and what is the default time | [Tech article](https://support.citrix.com/article/CTX223133?_ga=2.132411406.1854655211.1583708798-1865752561.1583708798) <br>Look at Get-ProvTask for information regarding the queue of stale disks. The default is every 6 hours. <br>It can be modified with these commands: <br>Set-ProvServiceConfigurationData -Name DiskReaper_retryInterval -Value 0:0:1  <br>Set-ProvServiceConfigurationData -Name DiskReader_heartbeatInterval -Value 0:0:1 
Clone on boot | Clone on boot means that the Citrix Hypervisor takes care of the creation of the new differenceing disks on boot instead of Citrix Apps and Desktops doing it
Memory and Disk cache settings when creating MCS Machine catalogs | [Great site that describes these settings](https://www.jgspiers.com/machine-creation-services-storage-ram-disk-cache/)
