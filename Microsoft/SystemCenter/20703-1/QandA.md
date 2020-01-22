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

## Date : 20 Jan 2020

Question  | Answer
---|---
What if some files need to be replaced after the installation of an Application | There are several ways to achieve this but one simple way is to setup the application with a deployment type of MSI and another deployment type for the script that will replace the files that are needed to execute the installed application. Set the Script to have a dependency for the MSI and then just make sure you are adding detection methods to ensure the MSI has installed before the script runs. Then you run the script deployment type to the devices and the dependency should take care of the rest
How do I change the target location of an application | This will send the installation to a different path: msiexec /passive TARGETDIR="D:\MyTargetDirectory" /i Software.msi
Can we get a quick report from powershell regarding the status of the Endpoint Security status | Get-Ciminstance -Namespace root/sms/Site_S01 -Classname SMS_EndpointProtectionHealthStatus
Which client is affected by what Maintenance Window | using the WMI classes SMS_Collection and SMS_FullCollectionMembership from the namespace root/sms/site_S01 you can determine which collection a device is in and from there you can determine which Maint Windows are in effect. 
