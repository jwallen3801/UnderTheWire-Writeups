# [Groot Level 10](https://underthewire.tech/groot-10)
## Description
"The password for groot11 is the one word that makes the two files on the desktop different.

**NOTE:**

– The password will be lowercase no matter how it appears on the screen."

## Solution
This level is pretty simple. All we really need to complete it is the [Compare-Object](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/compare-object?view=powershell-7.5) cmdlet. If we list the contents on the desktop, we see that we're provided with two text files: `old.txt` and `new.txt`. We can use `Compare-Object` to compare them. (For readers familiar with the Linux command line: this is similar to the `diff` command, only a little more verbose.) `Compare-Object` requires a `-ReferenceObject` and a `-DifferenceObject` parameter in order to compare them.

![image](https://github.com/user-attachments/assets/ea4c8f9f-b6fc-4bbc-b307-18966dd63b9b)

By default, `Compare-Object` only returns this difference indicator. To view the actual difference in content like the challenge description asks of us, we need to feed the contents of the respective files into `Compare-Object`.

![image](https://github.com/user-attachments/assets/e11fb1d6-cc61-4bb6-9663-bd2c90ab779a)

We can then use dot notation to grab the password and proceed to the next level.

![image](https://github.com/user-attachments/assets/21dafd05-1070-4bdf-a24a-d021d48e3b1b)

**Final command:** `(Compare-Object -ReferenceObject (Get-Content .\old.txt) -DifferenceObject (Get-Content .\new.txt)).InputObject`

**Password for groot11:** taserface
