# The Ripper
The guardian of this floor steps from the shadows. Known only as Jack the Ripper, he watches you carefully. He proclaims himself merciful and hands you a word list to help. He asks you to find the passcode hidden in this hash $2a$04$RNoyoWAcW0StwSri4YN1Eeb2j1gBNKutDOMxsLzfyfSvB/ghMHToa. The word list is your only aid. Only by combining the two correctly can you uncover the key and move on to the next floor.  
Flag format: citadel{password}

## My solve
**Flag:** `citadel{fake_flag_4_fake_pl4y3rs}`

I identified the hash format using an online hash identifier tool which revealed it to be a bcrypt hash with a cost factor of 4, making it relatively easier to crack. Using the provided word list, I ran a dictionary attack with tools like Hashcat or John the Ripper configured for bcrypt hashes. The cracking process matched a password from the word list whose bcrypt hash corresponded to the given hash. This password was the flag's password portion.

citadel{fake_flag_4_fake_pl4y3rs}

## What I learned
This challenge illustrated the practical implications of bcrypt's cost factor on hash security and cracking difficulty. It reinforced how to identify bcrypt hash formats and how to apply dictionary attacks effectively using cracking tools on bcrypt hashes.

## References
- Hash identifier tool: https://hashes.com/en/tools/hash_identifier


# AetherCorp NetprobeX
You step into a simulation of the past, entering the ruins of AetherCorp, the most ambitious corporation in history, and their creation, NetProbeX, once the most advanced networking tool the world had ever seen. The floor reconstructs the events that led to humanity’s downfall.

Your task is to find the hidden backdoor in NetProbeX, the flaw that triggered the collapse. By uncovering it, you can reverse the damage and retrieve the passcode to advance to the next floor.

Engineers left faint traces in the logs — small, odd markers where separators once sat. Read these traces as if they divide commands.

## My solve
**Flag:** `citadel{bl4ck51t3_4cc3ss_gr4nt3d}`

The challenge web interface suggested command injection by using `%0A` (URL-encoded newline) to chain commands. I started by listing files using the `ls` command to explore the directories. 

I found a file named `mission_briefing.txt`, which hinted the key was deeply hidden inside the AetherCorp network. Navigating to `/var/lib/aethercorp` I used `ls` to search its contents. 

Inside `/var/lib/aethercorp/archive/` I discovered a hidden directory `.secrets`, indicating the presence of sensitive files. Using the `ls` command revealed a file named `blacksite_key.dat`. 

Reading this file with `less` displayed the passcode. Thus, the final flag became: citadel{bl4ck51t3_4cc3ss_gr4nt3d}

## What I learned
This challenge highlighted practical use of command injection through newline character encoding to execute multiple shell commands. It also reinforced techniques for exploring Linux directory structures, accessing hidden files and directories, and the use of classic Linux commands like `ls` and `less` for enumeration and reading files during CTFs.

## References
- URL encoding and command injection fundamentals  
- Linux command line tools: ls, less
# Echoes and Pings
You come across the remnants of a fallen corporation and the final network communication ever sent by them.
Allegedly, the message contained an image that predicted the rise of the Citadel. Your task is to uncover what was sent and decode the communication to extract the passcode that will unlock the next floor.

## My solve
**Flag:** `citadel{1_r34lly_w4nt_t0_st4y_4t_y0ur_h0us3}`

Investigating the provided pcap file in Wireshark, I first checked the protocol hierarchy and noticed there were only 2 ICMP packets amid several TCP packets. Suspecting the “image” was hidden in ICMP, I examined those packets’ data. The first ICMP packet’s payload began with the JPEG magic bytes `ff d8 ff e0` (JFIF marker), and the second ended with `ff d9`, the JPEG EOF marker.

This suggested the raw bytes of a JPG image were exfiltrated via ICMP. To recover the image, I extracted the data from both ICMP packets and concatenated them, then saved the result as a `.jpg` file. Upon opening the file, the image contained the flag:# Echoes and Pings
You come across the remnants of a fallen corporation and the final network communication ever sent by them.
Allegedly, the message contained an image that predicted the rise of the Citadel. Your task is to uncover what was sent and decode the communication to extract the passcode that will unlock the next floor.

## My solve
**Flag:** `citadel{1_r34lly_w4nt_t0_st4y_4t_y0ur_h0us3}`

Investigating the provided pcap file in Wireshark, I first checked the protocol hierarchy and noticed there were only 2 ICMP packets amid several TCP packets. Suspecting the “image” was hidden in ICMP, I examined those packets’ data. The first ICMP packet’s payload began with the JPEG magic bytes `ff d8 ff e0` (JFIF marker), and the second ended with `ff d9`, the JPEG EOF marker.

This suggested the raw bytes of a JPG image were exfiltrated via ICMP. To recover the image, I extracted the data from both ICMP packets and concatenated them, then saved the result as a `.jpg` file. Upon opening the file, the image contained the flag:citadel{1_r34lly_w4nt_t0_st4y_4t_y0ur_h0us3}

## What I learned
This challenge demonstrated image exfiltration via a non-standard protocol (ICMP/ping) and reinforced skills in network forensics—specifically, identifying common file signatures (magic bytes) and reconstructing files transferred across split protocol packets.

## References
- File signatures: https://en.wikipedia.org/wiki/List_of_file_signatures
- Wireshark packet data extraction documentation








