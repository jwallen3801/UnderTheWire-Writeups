# [Century Level 7](https://underthewire.tech/century-7)
## Description
The password for Century8 is in a readme file somewhere within the contacts, desktop, documents, downloads, favorites, music, or videos folder in the user’s profile.

NOTE:

– The password will be lowercase no matter how it appears on the screen.

## Solution
This is the first level that requires us to leave the comfort of the desktop, so we start by backing out of it with `cd ..` in order to get the lay of the land in the root of the user directory.

![image](https://github.com/user-attachments/assets/fcb2c044-966a-400d-815e-653eb9fb44cf)

From here, we *could* manually search through all of the folders mentioned in the challenge description until we find the relevant file, but depending on how many subfolders there are, this could take a while. Instead, we can use [Get-ChildItem](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.management/get-childitem?view=powershell-7.5) to rescursively list all of the contents of all the directories while suppressing any errors in the output due to permissions and other issues.

![image](https://github.com/user-attachments/assets/ef236dd1-65f6-414c-8ed5-fb9c1d6e9ada)

The "recursive" part of this command means that it will return the contents every folder and subfolder beneath the current one, and this predictably results in a lot of output to the console, as there is a large tree of directories under our user account. Rather than sifting through all of this output, we can use PowerShell's [Where-Object](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/where-object?view=powershell-7.5) syntax to narrow down the results and return only what we're interested in. The challenge description says we're looking for a readme file, so we can use the `-like` operator to search for anything with "readme" in the name.

![image](https://github.com/user-attachments/assets/c7cc66d7-e106-440c-bd98-4fddde2f8752)

There is only one result, so this must be the file we're looking for. We can pipe the entire previous command to [Get-Content](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.management/get-content?view=powershell-7.5) to print the contents of the file to the console, which is the password for the next level.

![image](https://github.com/user-attachments/assets/180dc2a0-881a-499f-b33a-a9ced185cd33)

**Final command:** `Get-ChildItem -Force -Recurse -ErrorAction SilentlyContinue | Where {$_.Name -like "*readme*"} | Get-Content`

**Password for century8:** 7points
