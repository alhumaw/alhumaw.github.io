---
title: NahamCon CTF 2024 - Breath of the Wild
date: Sat May 25 10:20:00 AM +00 2024
categories: [Writeup]
tags: [ctf,forensics,nahamcon2024]
image: /assets/nahamconctf2024/icon.png
---
by `JohnHammond`

I got a sweet desktop background for my favorite video game, but now I want more! Problem is, I forget where I downloaded it from... can you help me remember where I got this old one?

Here's a backup of all my wallpapers. For security, I set the drive password to be videogames.

**Attachments**: 
[Breath-of-the-Wild](https://github.com/alhumaw/alhumaw.github.io/blob/main/assets/nahamconctf2024/breath-of-the-wild.7z)

## Solution
Pretty straightforward challenge, best done in Windows. The drive is a VHDX file, so just change the extension to that. Open the drive and unlock it with the password. There quite a few images that ultimately lead nowhere. The first step here is identifying that one of the files are a different dimension than the rest.


![xor](/assets/nahamconctf2024/link.png)

There also appear to be missing images according to the number naming scheme. Possibly deleted files? Time to check FTK Imager. 

If we take a closer look at each image, we can see that they each have a Zone.Identifier file attached. This file describes where the file was downloaded from.
Sure enough, if you check the Zone.Identifier of the image that had the odd resolution, the flag is there.

```
https://www.gamewallpapers.com/wallpapers_slechte_compressie/01wallpapers/&#102;&%23108;&%2397;&%23103;&%23123;&%2356;&%2351;&%23102;&%2350;&%2398;&%2348;&%2397;&%2356;&%2399;&%23101;&%2351;&%2357;&%23102;&%2350;&%23101;&%2353;&%2398;&%2397;&%2349;&%23100;&%2354;&%2399;&%2355;&%2348;&%23101;&%2357;&%2355;&%23102;&%2350;&%2357;&%2349;&%23101;&%23125
```

Decoding the URL:

```
https://www.gamewallpapers.com/wallpapers_slechte_compressie/01wallpapers/flag{83f2b0a8ce39f2e5ba1d6c70e97f291e}
```
