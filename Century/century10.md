# [Century Level 10](https://underthewire.tech/century-10)
## Description
"The password for Century11 is the 10th and 8th word of the Windows Update service description combined **PLUS** the name of the file on the desktop.

**NOTE:**

– The password will be lowercase no matter how it appears on the screen.

– If the 10th and 8th word of the service description is 'apple' and 'juice' and the name of the file on the desktop is '88', the password would be 'applejuice88'."

## Solution
This level is a significant step up in terms of difficulty. It took some more trial and error to find a solution compared to the earlier levels, especially while adhering to my constraint of finding a one-line solution that prints only the password to the console.

The obvious cmdlet to reach for when querying services is [Get-Service](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.management/get-service?view=powershell-7.5).

![image](https://github.com/user-attachments/assets/eb0610c1-b2bc-4936-98aa-1238101ac9cd)

There are too many services present on the system to easily browse through manually, so we can start to narrow it down with wildcard searches. The command `Get-Service *update*` doesn't return the service we're looking for, but the output does reveal a `DisplayName` property that can be further enumerated, and with this we can locate our Windows Update service from the challenge description.

![image](https://github.com/user-attachments/assets/99619753-0c08-433f-ac7f-f5176e2cc032)

This is where the `Get-Service` approach begins to hit a wall. It seems that no amount of options or other syntantic sugar can be added to the `Get-Service` cmdlet that will return the information required for this task (if any of you manage to find one, please let me know; I would be very interested to hear about it).

After googling around and perusing a few results from Stack Overflow, I discovered that the [Get-WmiObject](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.management/get-wmiobject?view=powershell-5.1) cmdlet must be used with the `win32_service` argument to achieve the verbosity required for obtaining the relevant information in this task. Searching on the "wuauserv" service we found with the previous command, we can pipe the output of `Get-WmiObject` to the [Format-List](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/format-list?view=powershell-7.5) cmdlet with a wildcard to retrieve all of the object's properties, where we finally find the service description we're looking for.

![image](https://github.com/user-attachments/assets/1545f6e3-4d6e-4557-8036-a5c9147c6f9f)

We can then isolate the string of the description with [Select-Object](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/select-object?view=powershell-7.5) and dot notation.

![image](https://github.com/user-attachments/assets/f5b4eab7-af67-4ff7-90af-d66d4114f486)

From here, it's just a matter of employing various string manipulation techniques. Similar to the previous level, we can use the `-split` option with bracket notation to grab the 10th and 8th words (remembering again to account for zero-based indexing). We can then add the [-Join](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_join?view=powershell-7.5) option with an empty string as an argument to print them as a single word.

![image](https://github.com/user-attachments/assets/834a3ae5-42a5-46eb-b212-a98d8b5d391a)

The challenge description states that the password must be lowercase, so we can append the `ToLower()` method to our command to ensure this. Finally, we need to concatenate the name of the file on the desktop to complete the password.

![image](https://github.com/user-attachments/assets/79b5333e-72f7-49d7-9a57-db61202daa2e)

**Final command:** `(((Get-WmiObject win32_service | Where {$_.Name -eq "wuauserv"} | Select Description).Description -split " ")[9,7] -join "").ToLower() + (gci).Name`

**Password for century11:** windowsupdates110
