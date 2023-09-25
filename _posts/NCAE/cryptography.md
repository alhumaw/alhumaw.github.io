---
title: NCAE 2023 - Crypto Railway
date: Mon Jul 24 06:56:00 PM +00 2023
categories: [Writeup]
tags: [ctf,cryptography]
---
by `NCAE`

I received this strange file in my inbox, but I have no idea how to read it! Can you help me figure out what it's telling me? This challenge is _twice_ the fun!
**Attachments**: 0x59325a744d5731756454426658324a7958326779657a4d334d325274646a646b6244526a4d324e6a583268665833417a6144417a4d54467964444233587a52715833497a645639736348303d

## Solution

This is the CTF challenge I solved that ultimately played a huge part in winning the 2023 NCAE Cyber Games.

First things first: 

plug this hex value into cyberchef, we get a base64 encoded message:
```
Y2ZtMW1udTBfX2JyX2gyezM3M2RtdjdkbDRjM2NjX2hfX3AzaDAzMTFydDB3XzRqX3IzdV9scH0=
```
Next:

plug this base 64 encoded message into cyberchef, We get this message:

```
cfm1mnu0__br_h2{373dmv7dl4c3cc_h__p3h0311rt0w_4j_r3u_lp}
```

After doing some research, this looked to be a railfence cipher:

In the rail fence cipher, the plaintext is written downwards diagonally on successive "rails" of an imaginary fence, then moving up when the bottom rail is reached, down again when the top rail is reached, and so on until the whole plaintext is written out. The ciphertext is then read off in rows.

So this is where we hit the crux of this challenge. After plugging this cipher into many auto decrypters we were unable to sucessfully pull the flag.

This ultimately led us to give up on the challenge until the last 30 minutes, where I read deeper into the hint:
```
This challenge is _twice_ the fun!
```

After playing with the railfence cipher, I came up with the thought that the cipher may just be railfence cipher'd _twice_, which in the end turned out to be the solution.

Using cryptii, if we set the orginal rail fence encrypted method to 2 key and 2 offset, grab that decoded message, then place it back in, we get the flag:


2 key 2 offset:
```
ccfcm_1hm_n_up03_h_0b3r1_1hr2t{03w7_34djm_vr73dul_4lcp3}
```

2 key 2 offset:
```
c2ctf{c0m3_w17h_m3_4nd_jump_0v3r_7h3_d0ubl3_r41l_c1ph3r}
```
