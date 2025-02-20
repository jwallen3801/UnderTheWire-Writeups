# [Century Level 5](https://underthewire.tech/century-5)
## Description
"The password for Century6 is the short name of the domain in which this system resides in **PLUS** the name of the file on the desktop.

**NOTE:**

– If the short name of the domain is 'blob' and the file on the desktop is named '1234', the password would be 'blob1234'.

– The password will be lowercase no matter how it appears on the screen."

## Solution
We can retrieve information about the domain with the [Get-ADDomain](https://learn.microsoft.com/en-us/powershell/module/activedirectory/get-addomain?view=windowsserver2025-ps) cmdlet. The first part of the password is visible in the output.

![image](https://github.com/user-attachments/assets/09cca53a-8c5d-4d5a-976f-339d5121bbdf)

We can grab the name with dot notation, then use the plus operator to concatenate it with the name of the file on the desktop.

![image](https://github.com/user-attachments/assets/34412f45-2178-42f6-8628-e8ebf5d121e5)

**Final command:** `(Get-ADDomain).Name + (gci).Name`

**Password for century6:** underthewire3347
