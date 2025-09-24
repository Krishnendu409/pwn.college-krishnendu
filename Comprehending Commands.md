# Commands / Filesystem — Full Module Writeups

# cat-not-the-pet-but-the-command
Read the flag file in your home directory using `cat`.

## My solve
**Flag:** `pwn.college{ACSdtdXKZxeC9-PM7fPaDqgpkBm.QXxcTN0wSN0EzNzEzW}`

I opened the flag file in my home directory using `cat flag` to display its contents.

WSL terminal session:
```wsl
hacker@commands~cat-not-the-pet-but-the-command:~$ cat flag
pwn.college{ACSdtdXKZxeC9-PM7fPaDqgpkBm.QXxcTN0wSN0EzNzEzW}
```

## What I learned
Simple use of `cat` to read files in the current directory; confirm file permissions before attempting more advanced reads.

## References
`man cat`; pwn.college challenge description.

---

# catting-absolute-paths
Read the flag at absolute path `/flag`.

## My solve
**Flag:** `pwn.college{Q_FoO4OIrYf7FziX7-Ek2eTbc-G.QX5ETO0wSN0EzNzEzW}`

I used `cat /flag` to read the file placed at an absolute path.

WSL terminal session:
```wsl
hacker@commands~catting-absolute-paths:~$ cat /flag
pwn.college{Q_FoO4OIrYf7FziX7-Ek2eTbc-G.QX5ETO0wSN0EzNzEzW}
```

## What I learned
Absolute paths let you read files regardless of current working directory (if permissions allow).

## References
Didn't use any reference.

---

# more-catting-practice
Read the flag at `/lib/maxima-sage/flag` by absolute path (no `cd` allowed).

## My solve
**Flag:** `pwn.college{cmIOmgjNjUeV9VJvwUsR9OFb_Xb.QXwITO0wSN0EzNzEzW}`

I used `cat /lib/maxima-sage/flag` to print the flag from that absolute path without changing directories.

WSL terminal session:
```wsl
hacker@commands~more-catting-practice:~$ cat /lib/maxima-sage/flag
pwn.college{cmIOmgjNjUeV9VJvwUsR9OFb_Xb.QXwITO0wSN0EzNzEzW}
```

## What I learned
You can access files anywhere by absolute path; `cd` is not required and may be disallowed by challenge constraints.

## References
`man cat`; pwn.college challenge description.

---

# grepping-for-a-needle-in-a-haystack
Search a large file for the flag using `grep`.

## My solve
**Flag:** `pwn.college{w-hKSEba41q8WKlw9prFqvJHMUq.QX3EDO0wSN0EzNzEzW}`

I searched `/challenge/data.txt` for the known prefix `pwn.college` with `grep`.

WSL terminal session:
```wsl
hacker@commands~grepping-for-a-needle-in-a-haystack:~$ grep pwn.college /challenge/data.txt
pwn.college{w-hKSEba41q8WKlw9prFqvJHMUq.QX3EDO0wSN0EzNzEzW}
```

## What I learned
`grep` is the right tool for extracting matching lines from very large files; use anchored or unique prefixes to narrow results.

## References
Didn't use any reference.

---

# comparing-files
Use `diff` to compare two files and reveal an added flag line.

## My solve
**Flag:** `pwn.college{0qJAH5CYiaFSvIqF01Ws8p7d_2O.01MwMDOxwSN0EzNzEzW}`

I ran `diff /challenge/decoys_only.txt /challenge/decoys_and_real.txt` and inspected the added line.

WSL terminal session:
```wsl
hacker@commands~comparing-files:~$ diff /challenge/decoys_only.txt /challenge/decoys_and_real.txt
47a48
> pwn.college{0qJAH5CYiaFSvIqF01Ws8p7d_2O.01MwMDOxwSN0EzNzEzW}
```

## What I learned
`diff` is useful to spot differences between files; added lines are typically marked with `a` and `>`.

## References
Didn't use any reference.

---

# listing-files:/challenge
List `/challenge` to find the renamed binary and run it.

## My solve
**Flag:** `pwn.college{ohEgkX_IKDOBUPECpvNyproB1VO.QX4IDO0wSN0EzNzEzW}`

I used `ls /challenge` to find the randomized filename and executed it by full path.

WSL terminal session:
```wsl
hacker@commands~listing-files:/challenge$ ls
26762-renamed-run-31782  DESCRIPTION.md

hacker@commands~listing-files:/challenge$ /challenge/26762-renamed-run-31782  DESCRIPTION.md
Yahaha, you found me! Here is your flag:
pwn.college{ohEgkX_IKDOBUPECpvNyproB1VO.QX4IDO0wSN0EzNzEzW}
```

## What I learned
`ls` reveals file names; execute discovered binaries with absolute paths to avoid PATH issues.

## References
Didn't use any reference

---

# touching-files:/tmp
Create `/tmp/pwn` and `/tmp/college` with `touch`, then run the checker.

## My solve
**Flag:** `pwn.college{EPls2GuUj6FzumQ4k6QUHgJ2KQn.QXwMDO0wSN0EzNzEzW}`

I created the required files in `/tmp` using `touch` and ran `/challenge/run` to confirm.

WSL terminal session:
```wsl
hacker@commands~touching-files:/tmp$ touch pwn
hacker@commands~touching-files:/tmp$ touch college
hacker@commands~touching-files:/tmp$ ls
bin  college  hsperfdata_root  pwn  tmp.TpSOPGOVKK
hacker@commands~touching-files:/tmp$ /challenge/run
Success! Here is your flag:
pwn.college{EPls2GuUj6FzumQ4k6QUHgJ2KQn.QXwMDO0wSN0EzNzEzW}
```

## What I learned
`touch` creates empty files; verify creates with `ls` before invoking checkers.

## References
Didn't use any reference

---

# linking-files
Make a symlink so a script that `cat`s a specific path prints the real flag.

## My solve
**Flag:** `pwn.college{YswdYPV9bvcq3lJ5MD88gNyH5mY.QX5ETN1wSN0EzNzEzW}`

I created a symlink from `/flag` to `/home/hacker/not-the-flag`, then ran the script that reads that fixed path.

WSL terminal session:
```wsl
hacker@commands~linking-files:~$ ln -s /flag /home/hacker/not-the-flag
hacker@commands~linking-files:~$ /challenge/catflag
About to read out the /home/hacker/not-the-flag file!
pwn.college{YswdYPV9bvcq3lJ5MD88gNyH5mY.QX5ETN1wSN0EzNzEzW}
```

## What I learned
Symbolic links (`ln -s`) let you satisfy programs/scripts that read fixed file paths by pointing those paths to the real file.

## References
Didn't use any reference

---

# removing-files
Delete the provided `delete_me` file and run the checker.

## My solve
**Flag:** `pwn.college{49Ve3S4H-QkQk8Sh5qShUYIhTmu.QX2kDM1wSN0EzNzEzW}`

I removed `delete_me` with `rm` and ran `/challenge/check` to receive the flag.

WSL terminal session:
```wsl
hacker@commands~removing-files:~$ ls
'Hello Hackers'  'Pondering Paths'   a   delete_me
hacker@commands~removing-files:~$ rm delete_me
hacker@commands~removing-files:~$ ls
'Hello Hackers'  'Pondering Paths'   a
hacker@commands~removing-files:~$ /challenge/check
Excellent removal. Here is your reward:
pwn.college{49Ve3S4H-QkQk8Sh5qShUYIhTmu.QX2kDM1wSN0EzNzEzW}
```

## What I learned
`rm` deletes files — double-check names before running; use `ls` to confirm deletion.

## References
Didn't use any reference

---

# moving-files
Move `/flag` into `/tmp/hack-the-planet` and run the checker.

## My solve
**Flag:** `pwn.college{8VvccP50i5QvxEjuQHdV2GxM4BS.0VOxEzNxwSN0EzNzEzW}`

I moved the global `/flag` to `/tmp/hack-the-planet` with `mv` and ran the checker to verify.

WSL terminal session:
```wsl
hacker@commands~moving-files:~$ mv /flag /tmp/hack-the-planet
Correct! Performing 'mv /flag /tmp/hack-the-planet'.
hacker@commands~moving-files:~$ /challenge/check
Congrats! You successfully moved the flag to /tmp/hack-the-planet! Here it is:
pwn.college{8VvccP50i5QvxEjuQHdV2GxM4BS.0VOxEzNxwSN0EzNzEzW}
```

## What I learned
`mv` renames/moves files; ensure destination path exists or use `mkdir -p` to create it first.

## References
`man mv`; filesystem move semantics.

---

# hidden-files
Find dot-prepended hidden files under `/` and read the flagged hidden file.

## My solve
**Flag:** `pwn.college{Y0jqHNbpcP7S8ATFRyck5nSPN9-.QXwUDO0wSN0EzNzEzW}`

I used `ls -a` to reveal hidden files in `/` and `cat`ed the discovered hidden flag file.

WSL terminal session:
```wsl
hacker@commands~hidden-files:~$ cd /
hacker@commands~hidden-files:/$ ls -a
.   .dockerenv            bin   challenge  etc   lib    lib64   media  nix  proc  run   srv  tmp  var
..  .flag-78701969019620  boot  dev        home  lib32  libx32  mnt    opt  root  sbin  sys  usr
hacker@commands~hidden-files:~/$ cat /.flag-78701969019620
pwn.college{Y0jqHNbpcP7S8ATFRyck5nSPN9-.QXwUDO0wSN0EzNzEzW}
```

## What I learned
Hidden files begin with `.` and are only shown by `ls -a`; they can hold important data or clues.

## References
Didn't use any reference

---

# an-epic-filesystem-quest
Follow a chain of clues (hidden/delayed/trapped) across many directories to the final flag.

## My solve
**Flag:** `pwn.college{UCH835FGbmepkr-SLzHHI4VvOwD.QX5IDO0wSN0EzNzEzW}`

I followed breadcrumb clues starting at `/`, used `ls -a` for hidden clues, `cd` when clues were delayed, and `cat` by full path for trapped clues. The final trapped clue revealed the flag.

WSL terminal session:
```wsl
krishnendu007@LAPTOP-8V0F4G2B:~$ ssh -i ~/key hacker@dojo.pwn.college
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
It is: pwn.college{UCH835FGbmepkr-SLzHHI4VvOwD.QX5IDO0wSN0EzNzEzW}
```

## What I learned
Combining `ls`, `ls -a`, `cd`, and `cat` is powerful for filesystem forensics; pay attention to instructions (hidden/delayed/trapped).

## References
Didn't use any reference

---

# making-directories (/tmp/pwn)
Create `/tmp/pwn`, add `college`, then run the checker.

## My solve
**Flag:** `pwn.college{4GKbJs93O5755UBKTE1J76U1jkj.QXxMDO0wSN0EzNzEzW}`

I created the directory, created the `college` file, and ran `/challenge/run` to get the flag.

WSL terminal session:
```wsl
hacker@commands~making-directories:~$ mkdir /tmp/pwn
hacker@commands~making-directories:~$ cd /tmp/pwn
hacker@commands~making-directories:/tmp/pwn$ touch college
hacker@commands~making-directories:/tmp/pwn$ /challenge/run
Success! Here is your flag:
pwn.college{4GKbJs93O5755UBKTE1J76U1jkj.QXxMDO0wSN0EzNzEzW}
```

## What I learned
`mkdir` creates directories and `touch` creates files inside them; checkers can require specific directory structure/filenames.

## References
Didn't use any reference

---

# finding-files (find)
Search the filesystem for files named `flag` and inspect them for the real flag.

## My solve
**Flag:** `pwn.college{k6SE6N6wjxu8ECKHFRP-kXNMSdS.QXyMDO0wSN0EzNzEzW}`

I ran `find / -name flag`, filtered candidate results, and `cat`ed the relevant file.

WSL terminal session:
```wsl
krishnendu007@LAPTOP-8V0F4G2B:~$ ssh -i ~/key hacker@dojo.pwn.college
Connected!
hacker@commands~finding-files:~$ find / -name flag
/usr/local/lib/python3.8/dist-packages/pwnlib/flag
/usr/lib/python3/dist-packages/sympy/integrals/rubi/tests/flag
... (other matches) ...
/nix/store/5qz6hgb1qzpvjrsw20wyiylx5zw8b9bk-pwntools-4.14.0/lib/python3.13/site-packages/pwnlib/flag

hacker@commands~finding-files:~$ cat /nix/store/5qz6hgb1qzpvjrsw20wyiylx5zw8b9bk-pwntools-4.14.0/lib/python3.13/site-packages/pwnlib/flag
pwn.college{k6SE6N6wjxu8ECKHFRP-kXNMSdS.QXyMDO0wSN0EzNzEzW}
```

## What I learned
`find` can search whole filesystem trees; expect and ignore permission-denied noise; focus on accessible results.

## References
Didn't use any reference

---


