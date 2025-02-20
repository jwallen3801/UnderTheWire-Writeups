# [Century Level 1](https://underthewire.tech/century-1)
## Description
"The password for Century2 is the **build version** of the instance of PowerShell installed on this system.

**NOTE:**

– The format is as follows: **.*.*****.****

– Include all periods

– Be sure to look for build version and NOT PowerShell version"

## Solution
As part of the default configuration, PowerShell stores a number of [automatic variables](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_automatic_variables?view=powershell-7.5). To solve this challenge, we can examine the [$PSVersionTable](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_automatic_variables?view=powershell-7.5#psversiontable) variable by simply typing its name into the console. The build version we're looking for is visible in the output.

![image](https://github.com/user-attachments/assets/32150e53-807c-411a-a841-92b7057d9774)

This is the correct answer to the challenge, but what if we want to print only the `BuildVersion` value to the console? If we attempt to access it with dot notation, it prints as a table.

![image](https://github.com/user-attachments/assets/76f3de4f-bf83-41f5-a3ec-3ef356895ea4)

However, we can use the [ToString()](https://learn.microsoft.com/en-us/dotnet/api/system.management.automation.psobject.tostring?view=powershellsdk-7.4.0) method to convert it to a string.

![image](https://github.com/user-attachments/assets/44fe9ccd-d034-48ad-a318-651719a69739)

**Final command:** `$PSVersionTable.BuildVersion.ToString()`

**Password for century2:** 10.0.14393.7604
