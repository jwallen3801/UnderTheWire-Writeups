# [Century Level 11](https://underthewire.tech/century-11)
## Description
"The password for Century12 is the name of the hidden file within the contacts, desktop, documents, downloads, favorites, music, or videos folder in the user’s profile.

**NOTE:**

– Exclude 'desktop.ini'.

– The password will be lowercase no matter how it appears on the screen."

## Solution
This level begins very similarly to level 7. We back out of the desktop and do a recursive listing of all the directories below the user root directory with `Get-ChildItem`. The only difference this time is that we add the `-Hidden` flag, because the challenge description specifies that it's a hidden file.

![image](https://github.com/user-attachments/assets/5c2c9620-4163-4805-a475-dbd9912b3b1e)

To narrow down the results, we can add the `-File` option to only return files, and since the challenge description says to exclude "desktop.ini", we can use `Where` syntax with the [-notmatch](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_comparison_operators?view=powershell-7.5#-match-and--notmatch) operator to exclude those results as well. (Note: the `-notmatch` operator uses [regex](https://en.wikipedia.org/wiki/Regular_expression) patterns.)

![image](https://github.com/user-attachments/assets/fa3efb02-e2b1-41c3-8557-8eec65834677)

Our challenge file is visible in the resulting output, so now we can just modify our command to only return what we want. Notable in this output is the fact that all of the hidden files except for the challenge file contain either the `.dat` or `.ini` file extensions somehwere in them. Leveraging this, we can modify the regex from the previous command into a more generic one that excludes all such results with `-notmatch`. (I prefer this approach to one of simply searching on the filename "secret_sauce" because it would work even if we didn't know the name of the challenge file or if it were changed at some point in the future.)

![image](https://github.com/user-attachments/assets/f632f063-4313-4428-ad83-1b43e3cf2b95)

This returns only the challenge file, allowing us to use dot notation as we have before to print the filename, which is the password for the next level.

**Final command:** `(Get-ChildItem -File -Hidden -Recurse -Force -ErrorAction SilentlyContinue | Where {$_.Name -notmatch "(\.ini|\.dat)"}).Name`

**Password for century12:** secret_sauce
