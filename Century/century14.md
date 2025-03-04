# [Century Level 14](https://underthewire.tech/century-14)
## Description
"The password for Century15 is the number of times the word 'polo' appears within the file on the desktop.

**NOTE:**

– You should count the instances of the whole word only.."

## Solution
This level is also quite simple, and only requires some creative use of the [Select-String](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/select-string?view=powershell-7.5) cmdlet. Its apparent simplicity is a little deceiving, though: as we'll see, it ends up being trickier than it appears at first glance.

Once again we have a file on the desktop containing a list of space-separated words, only this time it is much larger.

![image](https://github.com/user-attachments/assets/d783fd65-8356-4b50-a783-ddd25396dc9a)

We start with the command `gc .\countpolos | Select-String -Pattern "polo" -AllMatches` to return every line that contains the word "polo", but this isn't very helpful because the text file is all one big line, so it just prints the entire file again. We can use dot notation to only return the matches and how many of them there are.

![image](https://github.com/user-attachments/assets/f82ada8a-1e95-413b-9e2e-669df0c50c9a)
![image](https://github.com/user-attachments/assets/0c14980b-ee70-4623-b38e-bb985f1e715b)

At first this appears to be the answer, but if you attempt to use "158" as the password for century15, you'll quickly find that it is, in fact, incorrect. This is due to the problem hinted at in the challenge description: "you should count the instances of the **whole word only**" (emphasis mine). The way our command is currently written, it will return a match if the word is "polo" or if the word simply *contains* the word "polo" (e.g. "a**polo**gy").

Luckily, the `-Pattern` option of `Select-String` uses regular expressions for pattern matching, so we can add some regex magic to our pattern to only return matches that contain a space either before and after the string "polo", or only before it and ending with the string "polo". We have to include the latter because if you notice, the final word of the file is also "polo", so if you only search on "polo" with a space before and after, you'll once again come up with the slightly wrong answer of "152" because you'll be missing the final one, which only has a space before. The challenge creators appear to have done this on purpose to make sure we're *really* paying attention during the final level of the game.

![image](https://github.com/user-attachments/assets/c1cec48b-e0cf-4784-97dc-3c1f1b11604d)

**Final command:** `(gc .\countpolos | Select-String -Pattern "(\spolo\s|\spolo$)" -AllMatches).Matches.Count`

**Password for century15:** 153

## The End
And that's it! You can use the password to log in as century15 but there isn't really anything to do there. If we go to the [page](https://underthewire.tech/century-15) for Century 15 we're greeted with the following message:

"Congratulations!

You have successfully made it to the end!

Try your luck with other games brought to you by the Under The Wire team.

Thanks for playing!"
