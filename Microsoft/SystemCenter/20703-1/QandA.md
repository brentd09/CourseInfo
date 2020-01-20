# Questions and answers

## Date : 20 Jan 2020

Question  | Answer
---|---
Why Implement a Secondary site VS a Distribution Point | A secondary site may be usful if you have a large number of CM clients that are on the other side of a slow WAN link. Each CM Client needs to report to a Management Point and by creating a secondary site in the remote location the remote clients can pick up content from the secondary site DP and report to the secondary site MP. If you only created a DP at the remote location the reporting from each client would still need to get back to the promary site MP through the slow WAN. 
