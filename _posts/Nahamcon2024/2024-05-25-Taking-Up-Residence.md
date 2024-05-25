---
title: NahamCon CTF 2024 - Taking Up Residence
date: Sat May 25 11:20:00 AM +00 2024
categories: [Writeup]
tags: [ctf,forensics]
---
by `soups71`

My friend pulled this file during a recent incident response investigation.
He said it is probably just useless manifest data from a disk.

However, I think there might be some files that have taken up residence...

**Attachments**: 
![link](/assets/Evidence_001.zip)

## Solution
```
A resident file is a file that is the primary copy of a file and is stored on a disk, whether or not the disk is online. In computer forensics, a resident file can also be a file that only exists within the Master File Table (MFT) if the file is small.
```

This challenge is solved by opening the manifest data in Autopsy. For some reason, Linux Autopsy always works better for MFT data.

Once the drive is loaded, I dug around the filesystem to find anything peculiar by searching for strings containing flag.txt:

![xor](/assets/flag_txt.png)

Look like a python file that was stored in this MFT dump. The Base64 data is a powershell command that opens a file to grab a key.
Because the python script was executed and the script prints the key, the key also can be found in autopsy along with the encrypted flag

![xor](/assets/key.png)

![xor](/assets/encoded_flag.png)


We know the key and have the encrypted flag, just reverse the Fernet encryption to get the flag

```
flag{a4096cd70d8859d38cf8e7487b4cd0fa}
```
