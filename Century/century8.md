# [Century Level 8](https://underthewire.tech/century-8)
## Description
"The password for Century9 is the number of unique entries within the file on the desktop."

## Solution
This is a fairly straightforward level. On the desktop is a large text file containing a long list of random words.

![image](https://github.com/user-attachments/assets/c041878d-36d7-48db-9e0d-f27796ac9bdf)

Those familiar with the Linux command line will know that the best way to do this kind of task in bash is with the `sort` and `uniq` commands. PowerShell has its own counterparts in the [Sort-Object](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/sort-object?view=powershell-7.5) and [Get-Unique](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/get-unique?view=powershell-7.5) cmdlets (notice that the `Get-Unique` documentation says that the list must already be sorted for `Get-Unique` to work properly, so make sure to always use the two in combination).

![image](https://github.com/user-attachments/assets/3072b896-8772-4b9d-9333-20de7c293e53)

Now that we have our list of unique entries, we can use `Measure-Object` as we did in previous levels to get the number asked for in the challenge description, then use dot notation to print it to the console.

![image](https://github.com/user-attachments/assets/7fd798f1-9fb7-4e4f-a4b2-bd876675f2f4)

**Final command:** `(Get-Content .\unique.txt | Sort-Object | Get-Unique | Measure-Object).Count`

**Password for century9:** 696
