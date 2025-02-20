# [Century Level 2](https://underthewire.tech/century-2)
## Description
"The password for Century3 is the name of the built-in cmdlet that performs the wget like function within PowerShell **PLUS** the name of the file on the desktop.

**NOTE:**

– If the name of the cmdlet is “get-web” and the file on the desktop is named “1234”, the password would be “get-web1234”.

– The password will be lowercase no matter how it appears on the screen.

## Solution
This level is a bit different, as it doesn't really involve using commands to find the solution. The "built-in cmdlet that performs the wget like function within PowerShell" is called [Invoke-WebRequest](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/invoke-webrequest?view=powershell-7.5), and we can get the name of the file on the desktop with a simple `ls`.

![image](https://github.com/user-attachments/assets/710f085c-ba04-4521-9747-7f5975d6ed6d)

By combining the two and using lowercase, we have the password for century3.

**Final command:** N/A

**Password for century3:** invoke-webrequest443
