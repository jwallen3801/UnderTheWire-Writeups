# [Groot Level 2](https://underthewire.tech/groot-2)
## Description
"The password for groot3 is the word that is made up from the letters in the range of 1,481,110 to 1,481,117 within the file on the desktop.

**NOTE:**

– The password will be lowercase no matter how it appears on the screen."

## Solution
This level is very straightforward: there is a large text file on the desktop and we need to pull a single word out of it within the provided character index range. There are several possible solutions.

1. Using the same `Substring()` method from the solution for the previous level, we can simply plug in the character range given to us in the description. Recall that the `Substring()` method takes two parameters: the index of the character to start at and the length of the substring that you want.

![image](https://github.com/user-attachments/assets/5e28702c-355f-4658-81f9-25ead6e2728a)


2. Alternatively, we can use bracket notation with the range of the indexes of the letters along with the `-Join` option to concatenate them.

![image](https://github.com/user-attachments/assets/aaadaec9-029e-4a39-8f08-f589e7f2b6a3)


**Final command:** `(Get-Content \.elements.txt).Substring(1481110,7)`

OR

`(Get-Content \.elements.txt)[1481111..1481117] -Join ''`

**Password for groot3:** hiding
