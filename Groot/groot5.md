# [Groot Level 5](https://underthewire.tech/groot-5)
## Description
"The password for groot6 is the name of the workstation that the user with a username of 'baby.groot' can log into as depicted in Active Directory **PLUS** the name of the file on the desktop

**NOTE**:

– If the workstation is 'system1' and the file on the desktop is named '_log', the password would be 'system1_log'.

– The password will be lowercase no matter how it appears on the screen."

## Solution
To get information about a user in Active Directory, we can use the [Get-ADUser](https://learn.microsoft.com/en-us/powershell/module/activedirectory/get-aduser?view=windowsserver2025-ps) cmdlet, along with the username of the relevant user as a parameter to the `-Identity` option. If we're not sure about the exact name of the property we're looking for, we can pass an asterisk to the `-Properties` option as a wildcard to return everything.

![image](https://github.com/user-attachments/assets/d5e01b59-03d3-4326-9ae9-406eb6d97100)

This results in a fairly large list of properties, but scrolling through the output we eventually find the one that we're interested in from the challenge description.

![image](https://github.com/user-attachments/assets/bb9e0331-2171-4e12-9003-3510061c7f8e)

From here, it's only a matter of modifying our command to hone in on the specific property we want in our output, which we can do with dot notation. Finally, we can concatenate the output from the `ls` command to obtain the full, properly-formatted password as outlined in the challenge description.

![image](https://github.com/user-attachments/assets/3301df6b-8e77-4420-8a19-ed8ef8cbe3ca)


**Final command:** `(Get-ADUser -Identity "baby.groot" -Properties userWorkstations).userWorkstations + $(ls)`

**Password for groot6:** wk11_enterprise
