# [Groot Level 1](https://underthewire.tech/groot-1)
## Description
"The password for groot2 is the last five alphanumeric characters of the MD5 hash of this system’s hosts file.

**NOTE:**

– The password will be lowercase no matter how it appears on the screen."

## Solution
The most straighforward way to obtain a hash in PowerShell is with the [Get-FileHash](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/get-filehash?view=powershell-7.5) cmdlet. By default, `Get-FileHash` uses the SHA256 algorithm, but we can add the `-Algorithm` option to select a different one. In this case, we want the MD5 hash. On Windows systems, the hosts file can be found at `C:\Windows\System32\drivers\etc\hosts`. And thanks to PowerShell's object-oriented structure, we can use parentheses and dot notation to access the hash property of the resulting object so that only the hash is outputted to the console.

![image](https://github.com/user-attachments/assets/96f4ad89-78f6-494e-b35f-60387a1fa5c8)

The above output is sufficient to complete the level, as we can simply copy the last five characters of the hash and move on. However, we can modify the command to return only the characters we're interested in by adding the [Substring()](https://learn.microsoft.com/en-us/dotnet/api/system.string.substring?view=net-9.0) method. All MD5 hashes are 32 characters long, so we can input 27 and 5 as the parameters to `Substring()` to tell it to start at character 27 and end at character 32. And because the challenge description mentions that the password needs to be lowercase, we can add the [ToLower()](https://learn.microsoft.com/en-us/dotnet/api/system.string.tolower?view=net-9.0) method to our command for good measure to output the properly-formatted password to the console.

![image](https://github.com/user-attachments/assets/ea2a99e8-338a-476f-b0eb-6178df44755c)


**Final command:** `(Get-FileHash -Algorithm MD5 C:\Windows\System32\drivers\etc\hosts).Hash.Substring(27,5).ToLower()`

**Password for groot2:** 464c3
