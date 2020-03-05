# Questions and answers

## Date : 20 Jan 2020

Question  | Answer
---|---
Why Implement a Secondary site VS a Distribution Point | A secondary site may be usful if you have a large number of CM clients that are on the other side of a slow WAN link. Each CM Client needs to report to a Management Point and by creating a secondary site in the remote location the remote clients can pick up content from the secondary site DP and report to the secondary site MP. If you only created a DP at the remote location the reporting from each client would still need to get back to the promary site MP through the slow WAN. 

## Date : 21 Jan 2020

Question  | Answer
---|---
How to get the EndPoint Protection summary emailed as a report from SCCM | The best way to do this is with a custom report via SQL
How to create a license file to import to asset intelligence | [Microsoft Docs](https://docs.microsoft.com/en-us/configmgr/core/clients/manage/asset-intelligence/configuring-asset-intelligence) 

## Date : 03 Mar 2020

Question  | Answer
---|---
What if some files need to be replaced after the installation of an Application | There are several ways to achieve this but one simple way is to setup the application with a deployment type of MSI and another deployment type for the script that will replace the files that are needed to execute the installed application. Set the Script to have a dependency for the MSI and then just make sure you are adding detection methods to ensure the MSI has installed before the script runs. Then you run the script deployment type to the devices and the dependency should take care of the rest
How do I change the target location of an application | This will send the installation to a different path: msiexec /passive TARGETDIR="D:\MyTargetDirectory" /i Software.msi
Can we get a quick report from powershell regarding the status of the Endpoint Security status | Get-Ciminstance -Namespace root/sms/Site_S01 -Classname SMS_EndpointProtectionHealthStatus
Which client is affected by what Maintenance Window | using the WMI classes SMS_Collection and SMS_FullCollectionMembership from the namespace root/sms/site_S01 you can determine which collection a device is in and from there you can determine which Maint Windows are in effect. 
## Date : 3 Mar 2020

Question  | Answer
---|---
What happens if a collection is not given a "Maintenance Window" | The deployments and updates will occur whenever they are issued and will not be restricted to a time windows
## Date : 4 Mar 2020

Question  | Answer
---|---
What is the Harward history in the resource explorer | This is the results of the last 15 scans that were made for hardware inventory
Where can I find examples of asset intelligence license import files | [Example of an import file which needs to saved as a CSV file](https://docs.microsoft.com/en-us/configmgr/core/clients/manage/asset-intelligence/example-asset-intelligence-general-license-import)<br> [Technical specs of the file](https://docs.microsoft.com/en-us/configmgr/core/clients/manage/asset-intelligence/configuring-asset-intelligence)
How do SCCM clients know that other peer clients have the content they are requesting | The Peer client sends state messages back to the Management Point, this knowledge is then sent when a client requests the content from the MP [Microsoft Docs](https://docs.microsoft.com/en-us/configmgr/core/plan-design/hierarchy/client-peer-cache)
Application Dependencies and Requirements, what is the difference | A requirement tells SCCM which Deployment Type to deploy based on Hardware and/or O/S, the Dependency is Deployment type focused and will tell SCCM what software needs to be installed before a particular Deployment Type can be installed. [See Docs](https://docs.microsoft.com/en-us/configmgr/apps/understand/introduction-to-application-management) 
How do Deployment Type priorities work in SCCM | [They are evaluated in order and if triggered no other priority is evaluated](https://docs.microsoft.com/en-us/previous-versions/system-center/system-center-2012-R2/gg682031(v=technet.10)?redirectedfrom=MSDN)
Setting the Primary Device for a user can be set either from the Software Center tools or from SCCM via Automatic or Manual affinity settings | For the manual affinity it appears that the user must have logged in to that machine before they can be selected for affinity [Primary Device](https://docs.microsoft.com/en-us/configmgr/apps/deploy-use/link-users-and-devices-with-user-device-affinity)
## Date : 4 Mar 2020

Question  | Answer
---|---
How to clean up SCCM data to save space on the disk | Try using the Software Update Content Cleanup tool, IIS log cleanup tools, [Try this web site](http://eskonr.com/2016/08/sccm-configmgr-how-to-clean-ccmcache-content-older-than-x-days-using-compliance-settings/) and [this one too](https://www.systemcenterdudes.com/how-to-use-sccm-content-library-cleanup-tool/). You can write scripts to automate cleanup as well (be careful doing this) [Automate Orphaned content](https://www.scconfigmgr.com/2017/05/16/automating-content-library-content-clean-up/)
Which log file is for what? | [This is the official SCCM log reference](https://docs.microsoft.com/en-us/configmgr/core/plan-design/hierarchy/log-files)
Using CMTrace like a pro, merge multiple log files | [CMTrace merge logs](https://systoolbox.com/use-sccm-cmtrace-like-a-pro/15/)
How to test if the Management Point communication is working | [Use these URLs to determine if the MP is reponding](https://www.enhansoft.com/how-to-test-your-mp-to-confirm-if-it-is-healthy/)
