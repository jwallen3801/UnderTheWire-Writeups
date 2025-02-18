# [Groot Level 6](https://underthewire.tech/groot-6)
## Description
"The password for groot7 is the name of the program that is set to start when this user logs in **PLUS** the name of the file on the desktop.

**NOTE:**

– Omit the executable extension.

– If the program is 'mspaint' and the file on the desktop is named '_log', the password would be 'mspaint_log'.

– The password will be lowercase no matter how it appears on the screen."

## Solution
The obvious place to begin when looking for a program that is set to start when a user logs in is within the [Run and RunOnce keys](https://learn.microsoft.com/en-us/windows/win32/setupapi/run-and-runonce-registry-keys) of the registry. These keys are commonly abused by attackers to leave persistence mechanisms on a compromised machine, because whatever is placed in them will run every time the machine boots and the user logs in. Following the challenge description, we can start by inspecting the Run key for our current user in the `HKEY_CURRENT_USER (HKCU)` hive. The simplest way to inspect a registry key is with the `Get-Item` cmdlet. We immediately see the program mentioned in the challenge description, which follows the *Guardians of the Galaxy* theme of the game.

![image](https://github.com/user-attachments/assets/5655d0cf-08c7-4bf9-9ef1-23d3857fd59d)

We can then use dot and bracket notation to grab the relevant value before concatenating the output of the `ls` command to get the full value of the password as outlined in the challenge description.

![image](https://github.com/user-attachments/assets/3031cee4-1732-4450-a5bc-4d038a165c97)

**Final command:** `(Get-Item -Path HKCU:\Software\Microsoft\Windows\CurrentVersion\Run).Property[-1] + $(ls)`

**Password for groot7:** star-lord_rules
