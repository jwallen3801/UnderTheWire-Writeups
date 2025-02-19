# [Groot Level 9](https://underthewire.tech/groot-9)
## Description
"The password for groot10 is the name of the OU that doesn’t have accidental deletion protection enabled **PLUS** the name of the file on the desktop.

**NOTE:**

– If the name of the OU is called 'blue' and the file on the desktop is named '_bob', the password would be 'blue_bob'.

– The password will be lowercase no matter how it appears on the screen."

## Solution
This level deals with [Organizational Units](https://servicenow.iu.edu/kb?id=kb_article_view&sysparm_article=KB0026090) in Active Directory. Following a similar strategy to the previous level, we can use either tab completion, Google search, or `Get-Command` to quickly discover the [Get-ADOrganizationalUnit](https://learn.microsoft.com/en-us/powershell/module/activedirectory/get-adorganizationalunit?view=windowsserver2025-ps) cmdlet. To get an idea of how many objects we're working with, we'll once again make use of the `Measure-Object` cmdlet. The `Get-ADOrgranizationalUnit` cmdlet requires at least the `-Filter` parameter to return anything, so for now we'll just use a wildcard.

![image](https://github.com/user-attachments/assets/4cbf7aaa-7f18-49e1-8e1b-913ca27ae06a)

There are only 15 results, so it would actually be feasible to inspect all of them manually to find the solution, but we can do better than that. Ideally, when using a tool like PowerShell, we should aim for a solution that would work even if there were 1,500 or 15,000 results. The challenge description mentions that one of the OUs does *not* have accidental deletion protection enabled, so we can use [Select](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/select-object?view=powershell-7.5) to grab an example of one the objects, see if they have any `-Properties` related to this setting, and attempt to narrow our search from there.

![image](https://github.com/user-attachments/assets/5b1b3ce2-336a-4e31-a1fa-1fed2ca77803)

Sure enough, we have a `ProtectedFromAccidentalDeletion` property that appears to take a boolean as its value. Since we're looking for the OU where this property is *not* enabled, we can search on OU objects where this property is set to `False`. Doing so returns exactly one result.

![image](https://github.com/user-attachments/assets/afe4ee43-7300-4f04-82ab-f1f8b084daec)

This gives us the first part of the password. Because the challenge description mentions that the password must be lowercase, we can chain the `Tolower()` method with the `Name` property of the object before concatenating the name of the file on the desktop to complete the challenge.

![image](https://github.com/user-attachments/assets/db737191-0fe4-40f1-9406-82174ea6ccf4)

**Final command:** `(Get-ADOrganizationalUnit -Filter * -Properties * | Where {$_.ProtectedFromAccidentalDeletion -eq $False}).Name.Tolower() + (gci).Name`

**Password for groot10:** t-25_tester
