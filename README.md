# NexThink
How to create a custom NexThink powershell scripts and run it
NexThink uses PowerShell to run “remote actions”. Here is the documentation page https://doc.nexthink.com/Documentation/Nexthink/latest/UserManual/Writingscriptsforremoteactions 
You can build your own powershell script to gather some information from the workstations and / or do some actions. You need to sign this script and upload it to the NexThink client. Than you will be able to run it on multiple systems at one and get the result in a table. NOTE: NexThink doesn’t have any scheduler or task queue, so you will be able to get the results only from online systems. That means you may need to run it multiple times during the day and combine the results. 

1.	How to build a powershell script:
Add this line at the beginning of the script:
Add-Type -Path $env:NEXTHINK\RemoteActions\nxtremoteactions.dll
This will import the NXT library. Continue with the script execution. When you need to return any value use this construction:
[Nxt]::WriteOutputString("String_variable_name", $string_value)
[Nxt]::WriteOutputBool("Boolean_variable_name", $is_found)
More on variable types in the documentation (see link above). DO NOT use spaces or any special symbols (except “_”) in variable names.
IMPORTANT! NexThink has a known bug: uppercase $FALSE and $TRUE values causes process termination. Use lowercase ones (e.g. $false, $true). 

So overall approach here – build and test the script on your system using powershell tools. When ready – import the NXT library and convert all output to NXT format. 
2.	How to sign a script
NexThink will work only with company signed scripts or Vendor signed. See documentation for the details
3.	How to upload to NexThink
Open NexThink finder and login. Go to “Remote actions” and click “Create new remote action”. Please do this in your personal folder. 
 
Click “Import” and choose the signed powershell file. Pay attention to the checkboxes. 
4.	How to run the script on all systems
Go to “Start” -> “System statistic”
Choose all windows devices
Filter OS (remote actions are not supported in Win7)
Select all rows (Ctrl + A). 
Right click and choose your Remote Action
Wait few minutes, hit “refresh” (F5)
..and all done! Ctrl + A to select all data, Ctrl + C to copy and Ctrl + V to paste into the Excel
