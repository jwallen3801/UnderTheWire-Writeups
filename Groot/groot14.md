# [Groot Level 14](https://underthewire.tech/groot-14)
## Description
"The password for groot15 is the description of the share whose name contains 'task' in it **PLUS** the name of the file on the desktop.

**NOTE:**

– If the description is 'frozen_pizza' and the file on the desktop is named '_sucks', the password would be 'frozen_pizza_sucks'.

– The password will be lowercase no matter how it appears on the screen."

## Solution
We can list the shares on the system with the [Get-SmbShare](https://learn.microsoft.com/en-us/powershell/module/smbshare/get-smbshare?view=windowsserver2025-ps) cmdlet. There aren't many, and the share mentioned in the challenge description is easy to spot.

![image](https://github.com/user-attachments/assets/8f2ead13-e9a7-4a60-8c88-b290286e6d4b)

The rest should be familiar to anyone who's made it this far.

![image](https://github.com/user-attachments/assets/a82e52be-a3d8-47f5-bf6a-8458f8eb2925)

**Final command:** `(Get-SmbShare | Where {$_.Name -eq "Tasker"}).Description + (gci).Name`

**Password for groot15:** scheduled_things_8

## The End
And that's it! You can use the password to log in as groot15 but there isn't really anything to do there. If we go to the [page](https://underthewire.tech/groot-15) for Groot 15 we're greeted with the following message:

"Congratulations!

You have successfully made it to the end!

Try your luck with other games brought to you by the Under The Wire team.

Thanks for playing!"
