# [Century Level 4](https://underthewire.tech/century-4)
## Description
"The password for Century5 is the name of the file within a directory on the desktop that has spaces in its name.

**NOTE:**

– The password will be lowercase no matter how it appears on the screen."

## Solution
This is one of the easier levels, but it still deserves some explanation. As a general rule, it's recommended to not use spaces in file and directory names, as it can cause console errors and even lead to path exploitation vulnerabilities in some cases. But we can still access files and directories with spaces in their names easily. PowerShell has powerful tab completion, so if we simply use the [Get-ChildItem](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.management/get-childitem?view=powershell-7.5) cmdlet, start typing the name of the directory, and press the Tab key, PowerShell will automatically enclose it in quotes and complete the path for us.

![image](https://github.com/user-attachments/assets/f0691857-35cd-436c-b626-ee111630adc4)

We can then use parentheses and dot notation to nicely print the answer to the console.

**Final command:** `(gci '.\Can You Open Me').Name`

**Password for century5:** 6265
