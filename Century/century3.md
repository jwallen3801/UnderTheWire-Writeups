# [Century Level 3](https://underthewire.tech/century-3)
## Description
"The password for Century4 is the number of files on the desktop."

## Solution
In this level, we land on a desktop with a large number of random files and need to determine how many there are.

![image](https://github.com/user-attachments/assets/d576caba-9f75-4f59-87cd-375c52a056e1)

Counting them all manually would be both tedious and prone to error. Luckily, we have access to the [Measure-Object](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/measure-object?view=powershell-7.5) cmdlet, which can tell us exactly how many there are. To print the number to the console, which is also the answer to the challenge, we can use parentheses and dot notation to access the `Count` property of the object.

![image](https://github.com/user-attachments/assets/9653c3f5-c34b-491f-a829-ed14d7e9b2a7)

**Final command:** `(ls | Measure-Object).Count`

**Password for century4:** 123
