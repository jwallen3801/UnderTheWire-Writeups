# [Century Level 9](https://underthewire.tech/century-9)
## Description
"The password for Century10 is the **161st** word within the file on the desktop.

**NOTE:**

– The password will be lowercase no matter how it appears on the screen."

## Solution
This task also revolves around the manipulation of a text file.

![image](https://github.com/user-attachments/assets/be262685-9595-4167-a3f6-9989f4ebffe9)

In this case, the text file only contains a few hundred words, but even if it contained a million words and we had to locate the 161,000th word, the solution would be more or less the same.

First, we can use the [-Split](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_split?view=powershell-7.5) operator for strings to split this big blob of space-separated words into a neatly-formatted list. (Note that we have to place the output of the `Get-Content` cmdlet in parentheses to convert it to a string and enable the use of string methods on it.)

![image](https://github.com/user-attachments/assets/4d1206a0-9772-478e-ad40-ef102790167f)

We can add more parentheses to treat the resulting list like an array and then use bracket notation to access the 161st element. (Remember that we need to use one number below the one we want because of zero-based indexing.)

![image](https://github.com/user-attachments/assets/2a524591-7ff8-48e7-aac0-3f4b0855aef0)

**Final command:** `((gc .\Word_File.txt) -split " ")[160]`

**Password for century10:** pierid
