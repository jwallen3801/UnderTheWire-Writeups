# [Groot Level 4](https://underthewire.tech/groot-4)
## Description
"The password for groot5 is the name of the Drax subkey within the HKEY_CURRENT_USER (HKCU) registry hive.

NOTE:
– The password will be lowercase no matter how it appears on the screen."

## Solution
We need to find a subkey in the [registry](https://en.wikipedia.org/wiki/Windows_Registry), but from the description we have no idea where it is aside from the fact that it's somehwere within the `HKEY_CURRENT_USER` hive. However, we are given the name of the key, which makes searching for it much easier. We can use the `Get-ChildItem` cmdlet with the `-Recurse` option to recursively list every item in the `HKCU:\` path. The `-ErrorAction SilentlyContinue` option will prevent PowerShell from printing any ugly error messages to the console alongside our desired output, which tends to happen when recursively searching through a large directory space with normal user privileges. Finally, we can pipe the output to `Select-String` using the name of the subkey we already know from the challenge description.

![image](https://github.com/user-attachments/assets/c75d7ff6-5ffa-4ef9-b7c2-50023d3642f0)

By default, the `Select-String` cmdlet searches for the pattern case-insensitively, and we get both the Drax key and the subkey we're looking for in the ouput. This is sufficient to advence to the next level, but with a little more PowerShell-fu we can return only the string corresponding to the password for level 5. We can pipe the above output to `Select-Object` to grab the part with the path containing the subkey, then split the string with the `-Split` option and the backslash as a delimiter (note: because the backslash is a special character, we need to escape it with another backslash).

![image](https://github.com/user-attachments/assets/70bdd02a-3ba1-4b5a-a539-23e5ab85de1f)

Using bracket notation, the -1 index will return the last item in the resulting string array, which in this case is the password.

**Final command:** `((Get-ChildItem -Recurse -Path HKCU:\ -ErrorAction SilentlyContinue | Select-String -Pattern "drax" | Select-Object -Last 1) -Split "\\")[-1]`

**Password for groot5:** destroyer
