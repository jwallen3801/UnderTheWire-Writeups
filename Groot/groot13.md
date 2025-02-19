# [Groot Level 13](https://underthewire.tech/groot-13)
## Description
"The password for groot14 is the name of the Registered Owner of this system as depicted in the Registry **PLUS** the name of the file on the desktop.

**NOTE:**

– If the Registered Owner is 'Elroy' and the file on the desktop is named '_bob', the password would be 'elroy_bob'.

– The password will be lowercase no matter how it appears on the screen."

## Solution
With a bit of googling, we learn that the Registered Owner of a Windows system can be found in the registry under `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion` in a key named `RegisteredOwner`. We can then query this item using `Get-ItemProperty` with the `-Name` parameter.

![image](https://github.com/user-attachments/assets/109fe03f-7b9a-48df-9b3a-3941944e26ae)

The rest of the password can be completed using the same string manipulation techniques we've employed several times now, i.e. dot notation, the `ToLower()` method, and concatenating the name of the file on the desktop.

![image](https://github.com/user-attachments/assets/1ce8265d-cbd7-4ac8-a8ee-61ce06a80e92)

**Final command:** `(Get-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion' -Name "RegisteredOwner").RegisteredOwner + (gci).Name`

**Password for groot14:** utw_team_ned
