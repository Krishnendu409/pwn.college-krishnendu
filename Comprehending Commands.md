# Cat — Not the Pet, But the Command
Read the flag file in your home directory using cat.

## My solve
**Flag:** `pwn.college{ACSdtdXKZxeC9-PM7fPaDqgpkBm.QXxcTN0wSN0EzNzEzW}`

I opened the flag file in my home directory using `cat flag` to display its contents.

WSL terminal session:
"""hacker@commands~cat-not-the-pet-but-the-command:~$ cat flag
pwn.college{ACSdtdXKZxeC9-PM7fPaDqgpkBm.QXxcTN0wSN0EzNzEzW}"""

## What I learned
Basic use of `cat` to read files in the current directory.

## References
`man cat`, pwn.college challenge description.

---
# Cat an Absolute Path (/flag)
Read a file placed at absolute path `/flag` using `cat`.

## My solve
**Flag:** `pwn.college{Q_FoO4OIrYf7FziX7-Ek2eTbc-G.QX5ETO0wSN0EzNzEzW}`

I ran `cat /flag` to read the file at the absolute path.

WSL terminal session:
"""hacker@commands~catting-absolute-paths:~$ cat /flag
pwn.college{Q_FoO4OIrYf7FziX7-Ek2eTbc-G.QX5ETO0wSN0EzNzEzW}"""

## What I learned
Using absolute paths with `cat` (no need to change directories).

## References
`man cat`.

---
# Cat Hidden Flag in /lib
Read a flag located at `/lib/maxima-sage/flag` by absolute path.

## My solve
**Flag:** `pwn.college{cmIOmgjNjUeV9VJvwUsR9OFb_Xb.QXwITO0wSN0EzNzEzW}`

I used `cat /lib/maxima-sage/flag` to print the flag from that absolute path.

WSL terminal session:
"""hacker@commands~more-catting-practice:~$ cat /lib/maxima-sage/flag
pwn.college{cmIOmgjNjUeV9VJvwUsR9OFb_Xb.QXwITO0wSN0EzNzEzW}"""

## What I learned
Absolute paths let you read files anywhere you have permission to read.

## References
pwn.college challenge hint; `man cat`.

---
# Grep the Haystack
Search a very large text file for the flag using `grep`.

## My solve
**Flag:** `pwn.college{w-hKSEba41q8WKlw9prFqvJHMUq.QX3EDO0wSN0EzNzEzW}`

I used `grep` to search for the known flag prefix `pwn.college` in the provided data file.

WSL terminal session:
"""hacker@commands~grepping-for-a-needle-in-a-haystack:~$ grep pwn.college /challenge/data.txt
pwn.college{w-hKSEba41q8WKlw9prFqvJHMUq.QX3EDO0wSN0EzNzEzW}"""

## What I learned
`grep` is fast and convenient for finding lines containing a pattern in big files.

## References
`man grep`, pwn.college hint about flag prefix.

---
# Diff Reveals a Flag
Compare two files with `diff` to find a hidden flag line.

## My solve
**Flag:** `pwn.college{0qJAH5CYiaFSvIqF01Ws8p7d_2O.01MwMDOxwSN0EzNzEzW}`

I compared `/challenge/decoys_only.txt` and `/challenge/decoys_and_real.txt` with `diff` to reveal the extra line containing the flag.

WSL terminal session:
"""hacker@commands~comparing-files:~$ diff /challenge/decoys_only.txt /challenge/decoys_and_real.txt
47a48
> pwn.college{0qJAH5CYiaFSvIqF01Ws8p7d_2O.01MwMDOxwSN0EzNzEzW}"""

## What I learned
`diff` can expose added/removed lines between two files — useful for spotting hidden content.

## References
`man diff`.

---
# List Files to Find Renamed Binary
Use `ls` to discover a renamed `/challenge/run` and execute it.

## My solve
**Flag:** `pwn.college{ohEgkX_IKDOBUPECpvNyproB1VO.QX4IDO0wSN0EzNzEzW}`

I listed `/challenge` to find the randomly named binary, then executed it.

WSL terminal session:
"""hacker@commands~listing-files:/challenge$ ls
26762-renamed-run-31782  DESCRIPTION.md

hacker@commands~listing-files:/challenge$ /challenge/26762-renamed-run-31782  DESCRIPTION.md
Yahaha, you found me! Here is your flag:
pwn.college{ohEgkX_IKDOBUPECpvNyproB1VO.QX4IDO0wSN0EzNzEzW}"""

## What I learned
`ls` helps discover files when names are unknown; execute discovered binaries with full path.

## References
`man ls`.

---
# Create (touch) Files then Run Check
Create two files `/tmp/pwn` and `/tmp/college` with `touch` and run the checker.

## My solve
**Flag:** `pwn.college{EPls2GuUj6FzumQ4k6QUHgJ2KQn.QXwMDO0wSN0EzNzEzW}`

I created the files in `/tmp` and then ran `/challenge/run` which checks them.

WSL terminal session:
"""hacker@commands~touching-files:/tmp$ touch pwn
hacker@commands~touching-files:/tmp$ touch college
hacker@commands~touching-files:/tmp$ ls
bin  college  hsperfdata_root  pwn  tmp.TpSOPGOVKK
hacker@commands~touching-files:/tmp$ /challenge/run
Success! Here is your flag:
pwn.college{EPls2GuUj6FzumQ4k6QUHgJ2KQn.QXwMDO0wSN0EzNzEzW}"""

## What I learned
Creating files with `touch` and verifying challenge conditions with provided checkers.

## References
`man touch`.

---
# Remove delete_me and Get Reward
Delete the provided `delete_me` file and run the checker.

## My solve
**Flag:** `pwn.college{49Ve3S4H-QkQk8Sh5qShUYIhTmu.QX2kDM1wSN0EzNzEzW}`

I removed `delete_me` with `rm` and then ran `/challenge/check` to receive the flag.

WSL terminal session:
"""hacker@commands~removing-files:~$ ls
'Hello Hackers'  'Pondering Paths'   a   delete_me
hacker@commands~removing-files:~$ rm delete_me
hacker@commands~removing-files:~$ ls
'Hello Hackers'  'Pondering Paths'   a
hacker@commands~removing-files:~$ /challenge/check
Excellent removal. Here is your reward:
pwn.college{49Ve3S4H-QkQk8Sh5qShUYIhTmu.QX2kDM1wSN0EzNzEzW}"""

## What I learned
`rm` removes files; always double-check before deleting.

## References
`man rm`.

---
# Move /flag into /tmp/hack-the-planet (mv)
Move the global `/flag` into `/tmp/hack-the-planet` using `mv`, then run the checker.

## My solve
**Flag:** `pwn.college{8VvccP50i5QvxEjuQHdV2GxM4BS.0VOxEzNxwSN0EzNzEzW}`

I used `mv /flag /tmp/hack-the-planet` and then ran `/challenge/check` to confirm success and get the flag.

WSL terminal session:
"""hacker@commands~moving-files:~$ mv /flag /tmp/hack-the-planet
Correct! Performing 'mv /flag /tmp/hack-the-planet'.
hacker@commands~moving-files:~$ /challenge/check
Congrats! You successfully moved the flag to /tmp/hack-the-planet! Here it is:
pwn.college{8VvccP50i5QvxEjuQHdV2GxM4BS.0VOxEzNxwSN0EzNzEzW}"""

## What I learned
`mv` can move files across the filesystem; ensure destination exists or path is correct.

## References
`man mv`.

---
# Find the Dot-Prepended Hidden Flag in /
Discover dot-files with `ls -a` and read the hidden flag file at the root.

## My solve
**Flag:** `pwn.college{Y0jqHNbpcP7S8ATFRyck5nSPN9-.QXwUDO0wSN0EzNzEzW}`

I listed `/` with `ls -a` to reveal hidden dot files and then `cat`ed the revealed file.

WSL terminal session:
"""hacker@commands~hidden-files:~$ cd /
hacker@commands~hidden-files:/$ ls -a
.   .dockerenv            bin   challenge  etc   lib    lib64   media  nix  proc  run   srv  tmp  var
..  .flag-78701969019620  boot  dev        home  lib32  libx32  mnt    opt  root  sbin  sys  usr
hacker@commands~hidden-files:/$ cat /.flag-78701969019620
pwn.college{Y0jqHNbpcP7S8ATFRyck5nSPN9-.QXwUDO0wSN0EzNzEzW}"""

## What I learned
Hidden files start with `.` and must be revealed with `ls -a`. They can hide important data.

## References
`man ls`.

---
# An Epic Filesystem Quest (Breadcrumbs)
Follow a chain of clues across many directories (hidden/delayed/trapped) to reach the final flag.

## My solve
**Flag:** `pwn.college{UCH835FGbmepkr-SLzHHI4VvOwD.QX5IDO0wSN0EzNzEzW}`

I followed the breadcrumb clues starting at `/`, used `ls -a` for hidden clues, `cd` when a clue was delayed, and `cat` with full paths when clues were trapped (must not be `cd`ed into). Each clue pointed to the next directory; reading the final trapped clue gave the flag.

WSL terminal session (key successful steps only):
"""krishnendu007@LAPTOP-8V0F4G2B:~$ ssh -i ~/key hacker@dojo.pwn.college
Connected!
hacker@commands~an-epic-filesystem-quest:~$ cd /
hacker@commands~an-epic-filesystem-quest:/$ cat INFO
Tubular find!
The next clue is in: /usr/share/javascript/mathjax/unpacked/jax/output/SVG/fonts/Neo-Euler/Symbols

hacker@commands~an-epic-filesystem-quest:/usr/share/.../Symbols$ ls -a
.  ..  .CUE  Regular
hacker@commands~an-epic-filesystem-quest:/usr/share/.../Symbols$ cat .CUE
Congratulations, you found the clue!
The next clue is in: /usr/lib/tc

hacker@commands~an-epic-filesystem-quest:/usr/lib/tc$ cat INSIGHT
Great sleuthing!
The next clue is in: /opt/linux/linux-5.4/drivers/media/platform/qcom

hacker@commands~an-epic-filesystem-quest:/opt/.../qcom$ cat TEASER
Yahaha, you found me!
The next clue is in: /usr/share/icons/Humanity/apps/32
Watch out! The next clue is **trapped**.

hacker@commands~an-epic-filesystem-quest:/opt/.../qcom$ ls /usr/share/icons/Humanity/apps/32 | grep GIST
GIST-TRAPPED
hacker@commands~an-epic-filesystem-quest:/opt/.../qcom$ cat /usr/share/icons/Humanity/apps/32/GIST-TRAPPED
Congratulations, you found the clue!
The next clue is in: /usr/lib/python3/dist-packages/libfuturize/fixes

hacker@commands~an-epic-filesystem-quest:/usr/lib/.../fixes$ cat POINTER
Tubular find!
The next clue is in: /usr/share/rubygems-integration/all/gems/test-unit-3.3.5/lib/test/unit/ui/console

hacker@commands~.../console$ cat README
Congratulations, you found the clue!
The next clue is in: /usr/share/man/sk/man1/TIP

hacker@commands~.../man1$ cat /usr/share/man/sk/man1/TIP
Yahaha, you found me!
The next clue is in: /usr/share/emacs/26.3/etc/e/NUGGET-TRAPPED

hacker@commands~...$ cat /usr/share/emacs/26.3/etc/e/NUGGET-TRAPPED
CONGRATULATIONS! Your perserverence has paid off, and you have found the flag!
It is: pwn.college{UCH835FGbmepkr-SLzHHI4VvOwD.QX5IDO0wSN0EzNzEzW}"""

## What I learned
- How to combine `ls`, `ls -a`, `cd`, and `cat` to follow clues.  
- The difference between hidden, delayed (requires `cd`), and trapped clues (must `cat` by path).  
- Patience and careful navigation across deep system directories.

## References
pwn.college breadcrumb challenge; `man ls`, `man cat`, `man find`.

---
# Make /tmp/pwn and touch college
Create a directory `/tmp/pwn`, create a file `college` inside it, then run `/challenge/run`.

## My solve
**Flag:** `pwn.college{4GKbJs93O5755UBKTE1J76U1jkj.QXxMDO0wSN0EzNzEzW}`

I created the directory, created the `college` file, and ran the checker binary.

WSL terminal session:
"""hacker@commands~making-directories:~$ mkdir /tmp/pwn
hacker@commands~making-directories:~$ cd /tmp/pwn
hacker@commands~making-directories:/tmp/pwn$ touch college
hacker@commands~making-directories:/tmp/pwn$ /challenge/run
Success! Here is your flag:
pwn.college{4GKbJs93O5755UBKTE1J76U1jkj.QXxMDO0wSN0EzNzEzW}"""

## What I learned
`mkdir` creates directories; verify with `ls` and `cd` into them to operate inside.

## References
`man mkdir`, pwn.college.

---
# Find the Flag with find
Search the filesystem for files named `flag` and inspect the results to extract the real flag.

## My solve
**Flag:** `pwn.college{k6SE6N6wjxu8ECKHFRP-kXNMSdS.QXyMDO0wSN0EzNzEzW}`

I used `find / -name flag` to list every `flag` file, then examined the relevant file contents.

WSL terminal session (key lines only):
"""hacker@commands~finding-files:~$ find / -name flag
/usr/local/lib/python3.8/dist-packages/pwnlib/flag
/usr/lib/python3/dist-packages/sympy/integrals/rubi/tests/flag
... (other matches) ...
/nix/store/5qz6hgb1qzpvjrsw20wyiylx5zw8b9bk-pwntools-4.14.0/lib/python3.13/site-packages/pwnlib/flag

hacker@commands~finding-files:~$ cat /usr/lib/python3/dist-packages/sympy/integrals/rubi/tests/flag
pwn.college{k6SE6N6wjxu8ECKHFRP-kXNMSdS.QXyMDO0wSN0EzNzEzW}"""

## What I learned
`find` can search the whole filesystem for filenames; filter candidate results and inspect with `cat`.

## References
`man find`.

---
# Linking /flag to get output from cat script
Create a symlink so that a provided script reads `/flag` content into a different path the script prints; then execute it.

## My solve
**Flag:** `pwn.college{YswdYPV9bvcq3lJ5MD88gNyH5mY.QX5ETN1wSN0EzNzEzW}`

I created a symlink from `/flag` to `/home/hacker/not-the-flag` and then executed the challenge script to display the flag.

WSL terminal session (successful commands only):
hacker@commands~linking-files:~$ ln -s /flag /home/hacker/not-the-flag
hacker@commands~linking-files:~$ /challenge/catflag
About to read out the /home/hacker/not-the-flag file!
pwn.college{YswdYPV9bvcq3lJ5MD88gNyH5mY.QX5ETN1wSN0EzNzEzW}"""

## What I learned
Symbolic links (`ln -s`) can be used to make files available at other paths; scripts that `cat` a specific filename can be satisfied by linking.

## References
`man ln`, pwn.college challenge notes.

---
