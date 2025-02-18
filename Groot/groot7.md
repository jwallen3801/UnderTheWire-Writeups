# [Groot Level 7](https://underthewire.tech/groot-7)
## Description
"The password for groot8 is the name of the dll, as depicted in the registry, associated with the 'applockerfltr' service **PLUS** the name of the file on the desktop.

**NOTE:**

– The password will be lowercase no matter how it appears on the screen.

– If the name of the dll is “abc.dll” and the file on the desktop is named '_1234', the password would be 'abc_1234'."

## Solution
To search for information pertaining to a service within the registry, we can query the [HKLM\SYSTEM\CurrentControlSet\Services](https://learn.microsoft.com/en-us/windows-hardware/drivers/install/hklm-system-currentcontrolset-services-registry-tree) tree. Since the name of the service is given to us in the challenge description, we can query the key for that service directly by using the `Get-ItemProperty` cmdlet and appending the service's name to the path. Upon doing so, we immediately see the dll mentioned in the challenge description.

![image](https://github.com/user-attachments/assets/416fa53a-4e35-4ecb-b51f-55b7d5187f9a)

From here, we can use dot notation and follow an approach similar to the one we employed in level 4, using `-Split` to isolate the portion of the path that we want for the password and removing the `.dll` file extension with the `Substring()` method. Finally, we can once again concatenate the output of the `ls` command to append the name of the file on the desktop and complete the password.

![image](https://github.com/user-attachments/assets/113d449e-2a03-4f8b-8d96-442f0def8c3c)

**Final command:** `(((Get-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Services\applockerfltr).DisplayName) -Split "\\")[-1].Substring(0,6) + $(ls)`

**Password for groot8:** srpapi_home
