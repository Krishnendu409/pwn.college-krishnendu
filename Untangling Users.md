# becoming-root-with-su

type: become root using `su`

## My solve

**Flag:** `pwn.college{4I1AhP5fLfP5_M7de1-583VAyO5.QX1UDN1wSN0EzNzEzW}`

WSL terminal session:

```bash
hacker@users~becoming-root-with-su:~$ su
Password:
root@users~becoming-root-with-su:/home/hacker# cat /root/flag
cat: /root/flag: No such file or directory
root@users~becoming-root-with-su:/home/hacker# cat /root/flag
cat: /root/flag: No such file or directory
root@users~becoming-root-with-su:/home/hacker# cat /flag
pwn.college{4I1AhP5fLfP5_M7de1-583VAyO5.QX1UDN1wSN0EzNzEzW}
```

### My solve

Used `su` to switch to root. Looked for flags in `/root` and `/flag`. `/root/flag` did not exist. `/flag` contained the target string which I read with `cat /flag`.

### What I learned

`su` switches user context to root when you have the root password. Root's environment may not contain a `/root/flag`; always check other common locations like `/flag`.

---

# other-users-with-su

type: switch to another user with `su` and run their challenge

## My solve

**Flag:** `pwn.college{cDryDoq47tK5MdcGKdhrHocaNRX.QX2UDN1wSN0EzNzEzW}`

WSL terminal session:

```bash
hacker@users~other-users-with-su:~$ su zardus
Password:
zardus@users~other-users-with-su:/home/hacker$ /challenge/run
Congratulations, you have become Zardus! Here is your flag:
pwn.college{cDryDoq47tK5MdcGKdhrHocaNRX.QX2UDN1wSN0EzNzEzW}
```

### My solve

Used `su zardus` with the provided password to become the user `zardus`. Ran `/challenge/run` under that account to obtain the flag.

### What I learned

Switching to other users enables access to files and binaries restricted to their accounts. Keep credentials and user lists in mind when escalating or pivoting.

---

# cracking-passwords

type: crack leaked password hashes with `john` and use the recovered password

## My solve

**Flag:** `pwn.college{Q6tXN5y0SS_BhfVTn1Ji4D_zDWC.QX3UDN1wSN0EzNzEzW}`

WSL terminal session:

```bash
hacker@users~cracking-passwords:~$ john /challenge/shadow-leak
john --show /challenge/shadow-leak
su zardus
/challenge/run
Loaded 1 password hash (crypt, generic crypt(3) [?/64])
Press 'q' or Ctrl-C to abort, almost any other key for status
aardvark         (zardus)
1g 0:00:00:20 100% 2/3 0.04849g/s 282.3p/s 282.3c/s 282.3C/s Johnson..buzz
Use the "--show" option to display all of the cracked passwords reliably
Session completed
hacker:NO PASSWORD:20357:0:99999:7:::
zardus:aardvark:20371:0:99999:7:::

2 password hashes cracked, 0 left
Password:
zardus@users~cracking-passwords:/home/hacker$ /challenge/run
Congratulations, you have become Zardus! Here is your flag:
pwn.college{Q6tXN5y0SS_BhfVTn1Ji4D_zDWC.QX3UDN1wSN0EzNzEzW}
```

### My solve

Used `john` to crack the leaked shadow file. `john --show` revealed `aardvark` as `zardus`'s password. Used `su zardus` with that password and ran `/challenge/run` to get the flag.

### What I learned

`john` quickly cracks weak or unsalted hashes. When hashes are leaked, `john --show` reveals passwords to use for account takeover.

---

# using-sudo

type: demonstrate append vs truncate when redirecting output under `sudo`

## My solve

**Flags:**

* First-half shown in program output: `pwn.college{wIuC1lO2ZTA1q7-1MiErnFvAJtD.QX3ATO0wSN0EzNzEzW}`
* Final combined flag: `pwn.college{gncW8Nyhwx021zZuZOD9Tek7U62.QX3YTN0wSN0EzNzEzW}`
* Submission flag: `pwn.college{oF1Mb3Ip5OpbraLthnSmjFxxKv6.QX4UDN1wSN0EzNzEzW}`

WSL terminal session:

```bash
hacker@users~using-sudo:~$ sudo cat the-flag
sudo cat myflag
sudo cat MYFLAG
sudo cat not-the-flag
 |
\|/ This is the first half:
 v
pwn.college{wIuC1lO2ZTA1q7-1MiErnFvAJtD.QX3ATO0wSN0EzNzEzW}
                              ^
     that is the second half /|\
                              |

If you only see the second half above, you redirected in *truncate* mode (>)
rather than *append* mode (>>), and so the write of the second half to stdout
overwrote the initial write of the first half directly to the file. Try append
mode!

[FLAG] Here is your flag:
[FLAG] pwn.college{gncW8Nyhwx021zZuZOD9Tek7U62.QX3YTN0wSN0EzNzEzW}

pwn.college{oF1Mb3Ip5OpbraLthnSmjFxxKv6.QX4UDN1wSN0EzNzEzW}
```

### My solve

Observed that the program prints the first half and then a second half. When writing the second half to a file, using `>` can overwrite previous content. Instead use append redirection `>>` to concatenate. Viewed the combined flag and then the submission flag printed by the challenge.

### What I learned

`>` truncates files before writing. `>>` appends. Under `sudo` or redirected commands, use `>>` when you need to preserve earlier output.

---

## References

* `man su`
* `man john`
* `man sudo`
* `man bash` (I/O redirection)
