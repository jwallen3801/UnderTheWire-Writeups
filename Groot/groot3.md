# [Groot Level 3](https://underthewire.tech/groot-3)
## Description
"The password for groot4 is the number of times the word 'beetle' is listed in the file on the desktop."

## Solution
Similar to the previous level, we're provided with a very large text file. This time, we need to find the number of occurences of a word within the file. To do this, we can pipe the content of the file to the [Select-String](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/select-string?view=powershell-7.5) cmdlet, which comes with a number of powerful regular expression matching features. When used with the `-Pattern` and `-AllMatches` options, the `Select-String` cmdlet returns an object containing every occurence of a given pattern that it finds. We can use dot notation to access the match objects, which provides some useful information about each match that it found.

![image](https://github.com/user-attachments/assets/8cd3440a-95f2-4ee9-b52a-3faaa858b957)

Finally, we can get the count of the matches by drilling down further with dot notation.

![image](https://github.com/user-attachments/assets/6e42377b-a47f-44c6-bf24-8188972980dd)

**Final command:** `(Get-Content \.words.txt | Select-String -Pattern "beetle" -AllMatches).Matches.Count`

**Password for groot4:** 5
