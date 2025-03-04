# [Century Level 13](https://underthewire.tech/century-13)
## Description
"The password for Century14 is the number of words within the file on the desktop."

## Solution
This level is mercifully simple compared to some of the previous ones. All we really need to solve it is our old friend `Measure-Object`. The file on the desktop is just a large list of space-separated words.

![image](https://github.com/user-attachments/assets/40587b0c-1927-4430-af58-f336cf99754f)

To count them,  we can simply pipe the output of `Get-Content` into `Measure-Object` with the `-Word` option, then use dot notation to print the number, which in this case is the password.

![image](https://github.com/user-attachments/assets/a5a8d504-8909-488c-9d90-d8466adab02a)

**Final command:** `(gc .\countmywords | Measure-Object -Word).Words`

**Password for century14:** 755
