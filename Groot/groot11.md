# [Groot Level 11](https://underthewire.tech/groot-11)
## Description
"The password for groot12 is within an alternate data stream (ADS) somewhere on the desktop.

**NOTE:**

– The password will be lowercase no matter how it appears on the screen."

## Solution
[Alternate data streams](https://en.wikipedia.org/wiki/NTFS#Alternate_data_stream_(ADS)) are an interesting feature of the Windows NTFS file system that allow for additional data streams to be associated with a filename, typically for storing metadata. In PowerShell, the `Get-Item` and `Get-Content` cmdlets can be used with the `-Stream` parameter to access these otherwise invisible data streams, which can contain additional data not found in the file they're attached to. To view an example of this, we can inspect one of the files provided in the challenge directory using the aforementioned `-Stream` parameter.

![image](https://github.com/user-attachments/assets/2e2a8d03-7ea9-49ff-8449-adda402cabf2)

We can use wildcards and `Select` to view the all of the filenames and their associated data streams simultaneously. One of them stands out as the likely target of the challenge.

![image](https://github.com/user-attachments/assets/4f76bf4b-4b9f-4ff2-8ec8-36f5ac318b04)

The contents of the stream can be read by passing its name as an argument to `Get-Content`.

![image](https://github.com/user-attachments/assets/37f85a91-c32d-43ea-a56c-d5c213dec6a3)

**Final command:** `Get-Content .\TPS_Reports04.pdf -Stream "secret"`

**Password for groot12:** spaceships

### BONUS solution
In my quixotic mission to craft neat little one-line solutions for all of these challenges, I came up with a much more convoluted solution for this level that has the advantage of working even if we didn't know which file contained the secret stream or the name of the stream itself. Unfortunately, the `-Stream` parameter doesn't accept wildcards when used with `Get-Content`, and it took a fair amount of trial and error to find a way around this. I leave it here for your consideration.

![image](https://github.com/user-attachments/assets/e3b24003-2e8d-404f-b247-ff38c749c94b)
