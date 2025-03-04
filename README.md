# Under the Wire Writeups
This repository contains my walkthroughs for completing the [PowerShell wargames from Under the Wire](https://underthewire.tech/wargames). The target audience for these writeups is other IT and cybersecurity enthusiasts who want to learn some cool PowerShell tricks along with me. While I attempt to be thorough and link to relevant documentation where applicable, some basic knowledge about using the command line is either assumed or passed over without explanation, such as using the pipe character `|` to chain commands together or using [aliases for cmdlets in PowerShell](https://learn.microsoft.com/es-es/powershell/module/microsoft.powershell.core/about/about_aliases?view=powershell-7.5) (e.g. `ls` or `gci` instead of `Get-ChildItem`). Any such explanations that aren't explicitly included are easily discoverable with a search engine.

To make these solutions a little more interesting for both myself and you, I've placed the following constraints on myself for what I will consider to be an adequate solution:

1. The solution for every level must consist of a single line of PowerShell.
2. It must output nothing to the console except the correct answer, which is always the properly-formatted password to the next level.

I attempt to do this even when it would be more convenient to simply copy some portion of the output which contains the password or part of the password. I also try to avoid relying on hard-coded values if a more generic option is available so that the solution would remain valid even if the names of those values were to change. I believe this will force me to be more creative with my PowerShell commands than a given task or challenge may necessarily require, and will hopefully result in more interesting solutions for the reader. That being said, feel free to borrow from these solutions at any step along the way, as many of them will provide the correct answer at some intermediate stage before arriving at my final solution.

I've omitted solutions for level 0 -> level 1 of every game, as the password is always just the username for level 1 (i.e. century1, cyborg1, groot1, etc.). Every other level can be accessed through SSH with some variation of:
```
$ ssh <level_name>@<game_name>.underthewire.tech 
```
along with the password for that level. See the instructions on the Under the Wire site if this is unclear.

With all of that out of the way, have fun! I hope these writeups will be useful to other PowerShell learners. I don't claim any authority or expertise on the subject, and I welcome any feedback or suggestions.
