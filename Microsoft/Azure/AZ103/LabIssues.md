# Lab Issues

LabNumber | Step | Problem | Fix
---|---|---|---
4 | ? | When running Import-Module command the Module it loads the wrong module version|Allow the module to autoload by skipping the Import-Command and go straight on to launch the powershell command which autoloads the correct module version, there appears to be a bug in PS that loads modules with the same name from different locations based on whether you for the import or autoload the module.
6 | ? | Second VM will not create | Place the first resource group and VM in East US and the second resource group and VM  in SE Asia these two regions seem to work for the lab


