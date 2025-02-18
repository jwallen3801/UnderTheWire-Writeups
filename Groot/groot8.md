# [Groot Level 8](https://underthewire.tech/groot-8)
## Description
"The password for groot9 is the description of the firewall rule blocking MySQL **PLUS** the name of the file on the desktop.

**NOTE:**

– If the description of the rule is 'blue' and the file on the desktop is named '_bob', the password would be 'blue_bob'.

– The password will be lowercase no matter how it appears on the screen."

## Solution
This level feels like a good opportunity to showcase the fact that, given an administrative action that can be performed in Windows, there's probably an obvious PowerShell cmdlet for it, and even if you don't know what it is, chances are you can find it with either the [Get-Command](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/get-command?view=powershell-7.5) cmdlet and a wildcard search, tab completion, or by simply googling it. Since we're ideally looking for a cmdlet that can query firewall rules, we can use `Get-Command` to search for any cmdlet containing the word "firewall" and see what comes back.

![image](https://github.com/user-attachments/assets/59417668-fb89-41b5-b93f-bb62f3f5bf90)

Sure enough, we discover that there's an aptly-named [Get-NetFirewallRule](https://learn.microsoft.com/en-us/powershell/module/netsecurity/get-netfirewallrule?view=windowsserver2025-ps) cmdlet. Using our handy new cmdlet, we can retrieve all the firewall rules on the system. But if there are a lot of firewall rules present in the configuration, this output will be a bit overwhelming, so first we'll pipe it to the [Measure-Object](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/measure-object?view=powershell-7.5) cmdlet to get an idea of how many rules we're working with.

![image](https://github.com/user-attachments/assets/bdaf6ceb-56da-4a0c-895e-61da54b6561e)

As I suspected, there are enough rules present (304) to make it both inconvenient and inefficient to sift through them all manually, hoping to spot our answer from the challenge description. While it's technically possible to do so, it would be tedious and time-consuming, and we should consider it only as a last resort. Luckily, the description includes a hint that the rule deals with MySQL, so we can see what properties the firewall rule objects have by looking at one of them and then use PowerShell's [Where](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/where-object?view=powershell-7.5) syntax to see if any of them have a property containing a reference to MySQL. By using `Where` with the `-like` operator, we can perform wildcard searches for MySQL on different properties until we find a match. We quickly discover that exactly one firewall rule object has a `DisplayName` property containing MySQL.

![image](https://github.com/user-attachments/assets/886efa05-940d-49be-a822-0763ead8b87d)

This same firewall rule object contains the `Description` property mentioned in the challenge description, which we can access with dot notation and then concatenate with the name of the file on the desktop as we've done in previous levels.

![image](https://github.com/user-attachments/assets/f3d8c448-c253-46f5-b5c1-b74707464972)

**Final command:** `(Get-NetFirewallRule | Where {$_.DisplayName -like "*mysql*"}).Description + $(ls)`

**Password for groot9:** call_me_starlord
