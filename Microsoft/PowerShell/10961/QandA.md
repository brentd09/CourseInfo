# Questions and answers

## Date : 

Question  | Answer
---|---
When running external commands, does PowerShell wait for the external command to finish before passing the results to the PowerShell window | It appears if you execute a ping -t IP that the information is streamed to the PS window in real time
Why do background jobs fail when they reference relative path-names | When the background job is run the runspace that is opened for the session sets the default location to your Documents folder under your profile.
