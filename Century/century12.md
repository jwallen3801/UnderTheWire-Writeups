# [Century Level 12](https://underthewire.tech/century-12)
## Description
"The password for Century13 is the description of the computer designated as a Domain Controller within this domain **PLUS** the name of the file on the desktop.

**NOTE:**

– The password will be lowercase no matter how it appears on the screen.

– If the description 'today_is' and the file on the desktop is named '_cool', the password would be 'today_is_cool'."

## Solution
At first I assumed that the proper cmdlet for this level would be [Get-ADDomainController](https://learn.microsoft.com/en-us/powershell/module/activedirectory/get-addomaincontroller?view=windowsserver2025-ps), as that's ostensibly what we're after. However, no amount of options added to this command, nor techniques such as piping it to `Format-List` with a wildcard as we did earlier, seem to return the "description" property mentioned in the challenge description.

![image](https://github.com/user-attachments/assets/6fd19f33-1068-43a4-9d02-667b6b5ae279)

If you keep searching for other cmdlets that might be applicable in this situation, you'll eventually stumble across [Get-ADComputer](https://learn.microsoft.com/en-us/powershell/module/activedirectory/get-adcomputer?view=windowsserver2025-ps). The first example shown in the documentation is particularly instructive in this case. We already got the name of the DC computer from the previous `Get-ADDomainController` command, so we can plug that into `Get-ADComputer` and list all of its properties.

![image](https://github.com/user-attachments/assets/ae34c710-ed1d-4aeb-a4e7-92588bf603e4)

In the resulting output, we see our elusive "Description" property, and from here it's simply a matter of accessing it with dot notation and concatenating the name of the file on the desktop as we've done in other levels. Everything is already in lowercase so we don't need to bother with `ToLower()` this time.

![image](https://github.com/user-attachments/assets/a7705a80-672c-43cf-b85f-174a97eadd62)

**Final command:** `(Get-ADComputer -Identity (Get-ADDomainController).Name -Properties Description).Description + (gci).Name`

**Password for century15:** i_authenticate_things
