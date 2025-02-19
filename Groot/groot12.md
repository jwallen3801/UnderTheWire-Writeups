# [Groot Level 12](https://underthewire.tech/groot-12)
## Description
"The password for groot13 is the owner of the Nine Realms folder on the desktop.

**NOTE:**

– Exclude the Administrator, the Administrators group, and System.

– The password will be lowercase with no punctuation no matter how it appears on the screen. For example, if the owner is 'john.doe', it would be 'johndoe'."

## Solution
All we really need to solve this challenge is the [Get-Acl](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.security/get-acl?view=powershell-7.5) cmdlet, which provides some basic security information about a given resource, including the owner, which is what we want in this case.

![image](https://github.com/user-attachments/assets/42e3dc39-db90-44b4-8030-39f9ef370bd1)

From here, we can follow a similar process seen in previous levels of using dot and bracket notation, `-Split`, and `ToLower()` to output the correctly-formatted password to the console.

![image](https://github.com/user-attachments/assets/baf7905d-4056-4c23-b703-6aa9a9568875)

**Final command:** `(((Get-Acl '.\Nine Realms').Owner) -split "\\")[-1].ToLower()`

**Password for groot13:** airwolf
