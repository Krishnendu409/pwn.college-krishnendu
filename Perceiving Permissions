# changing-file-ownership

type: change file owner with `chown`

## My solve

**Flag:** `pwn.college{sHTcJ8xc8gLbMy-wBxzz20_hmed.QXxEjN0wSN0EzNzEzW}`

WSL terminal session:

```bash
hacker@permissions~changing-file-ownership:~$ ls -l /flag
-r-------- 1 root root 60 Oct 10 19:39 /flag
hacker@permissions~changing-file-ownership:~$ chown hacker /flag
hacker@permissions~changing-file-ownership:~$ ls -l /flag
-r-------- 1 hacker root 60 Oct 10 19:39 /flag
hacker@permissions~changing-file-ownership:~$ cat /flag
pwn.college{sHTcJ8xc8gLbMy-wBxzz20_hmed.QXxEjN0wSN0EzNzEzW}
```

### My solve

Changed owner of `/flag` to `hacker` using `chown hacker /flag`. Then read the file with `cat /flag` to get the flag.

### What I learned

`chown` changes file ownership when you have sufficient privileges. Ownership affects who can read files even when permissions are restrictive.

---

# groups-and-files

type: change group ownership with `chgrp`

## My solve

**Flag:** `pwn.college{8-WRujb3CLeXrzmk9WyE1xot7jR.QXxcjM1wSN0EzNzEzW}`

WSL terminal session:

```bash
hacker@permissions~groups-and-files:~$ id
uid=1000(hacker) gid=1000(hacker) groups=1000(hacker)
hacker@permissions~groups-and-files:~$ ls -l /flag
-r--r----- 1 root root 60 Oct 10 19:46 /flag
hacker@permissions~groups-and-files:~$ chgrp hacker /flag
hacker@permissions~groups-and-files:~$ ls -l /flag
-r--r----- 1 root hacker 60 Oct 10 19:46 /flag
hacker@permissions~groups-and-files:~$ cat /flag
pwn.college{8-WRujb3CLeXrzmk9WyE1xot7jR.QXxcjM1wSN0EzNzEzW}
```

### My solve

Used `chgrp hacker /flag` to change the file's group to one the user belongs to. Then read the file.

### What I learned

`chgrp` adjusts group ownership. Group membership plus group permissions can grant access without changing owner.

---

# fun-with-groups-names

type: change group to a numeric or custom group name

## My solve

**Flag:** `pwn.college{<no-flag-shown>}`

WSL terminal session:

```bash
hacker@permissions~fun-with-groups-names:~$ id
uid=1000(hacker) gid=1000(grp10525) groups=1000(grp10525)
hacker@permissions~fun-with-groups-names:~$ ls -l /flag
-r--r----- 1 root root 60 Oct 10 19:49 /flag
hacker@permissions~fun-with-groups-names:~$ chgrp grp10525 /flag
hacker@permissions~fun-with-groups-names:~$ ls -l /flag
-r--r----- 1 root grp10525 60 Oct 10 19:49 /flag
hacker@permissions~fun-with-groups-names:~$ cat /flag

```

### My solve

Changed the file's group to `grp10525` which the current user belongs to. After that the user could access the file per group permissions.

### What I learned

Numeric or unusual group names are valid. Check `id` to confirm group membership before changing group ownership.

---

# changing-permissions

type: modify file mode with `chmod` to grant others read

## My solve

**Flag:** `pwn.college{4fkmcJM4tkTbjbLQXjMd3PByxx0.QXzcjM1wSN0EzNzEzW}`

WSL terminal session:

```bash
hacker@permissions~changing-permissions:~$ ls -l /flag
-r-------- 1 root root 60 Oct 10 19:51 /flag
hacker@permissions~changing-permissions:~$ chmod o+r /flag
hacker@permissions~changing-permissions:~$ ls -l /flag
-r-----r-- 1 root root 60 Oct 10 19:51 /flag
hacker@permissions~changing-permissions:~$ cat /flag
pwn.college{4fkmcJM4tkTbjbLQXjMd3PByxx0.QXzcjM1wSN0EzNzEzW}
```

### My solve

Used `chmod o+r /flag` to add read permission for "others" then read the flag.

### What I learned

`chmod` can modify owner/group/other permissions. `o+r` adds read for others. Be cautious when altering permissions on sensitive files.

---

# executable-files

type: add execute bit for owner with `chmod u+x`

## My solve

**Flag:** `pwn.college{0yftxv1h0zdYmUc__ngJ1vL1UnF.QXyEjN0wSN0EzNzEzW}`

WSL terminal session:

```bash
hacker@permissions~executable-files:~$ ls -l /challenge/run
-r--r--r-x 1 hacker hacker 32 Jan 14  2025 /challenge/run
hacker@permissions~executable-files:~$ chmod u+x /challenge/run
hacker@permissions~executable-files:~$ ls -l /challenge/run
-r-xr--r-x 1 hacker hacker 32 Jan 14  2025 /challenge/run
hacker@permissions~executable-files:~$ /challenge/run
Successful execution! Here is your flag:
pwn.college{0yftxv1h0zdYmUc__ngJ1vL1UnF.QXyEjN0wSN0EzNzEzW}
```

### My solve

Set the user execute bit with `chmod u+x /challenge/run`, then executed the binary to retrieve the flag.

### What I learned

Owner execute permission allows running a file as a program. File must also be a valid executable.

---

# permission-tweaking-practice

type: iterative `chmod` challenges to match required modes

## My solve

**Flag:** `pwn.college{Qd3xbLqKp_jHv490XNBuP38Svki.QXwEjN0wSN0EzNzEzW}`

WSL terminal session excerpts:

```bash
# multiple rounds adjusting /challenge/pwn permissions with chmod to match required masks
hacker@permissions~permission-tweaking-practice:~$ chmod u=rw,g=rx,o=rx /challenge/pwn
hacker@permissions~permission-tweaking-practice:~$ chmod a+r /flag
hacker@permissions~permission-tweaking-practice:~$ ls -l /flag
-r--r--r-- 1 hacker hacker 60 Oct 10 19:56 /flag
hacker@permissions~permission-tweaking-practice:~$ cat /flag
pwn.college{Qd3xbLqKp_jHv490XNBuP38Svki.QXwEjN0wSN0EzNzEzW}
```

### My solve

Completed the eight chmod rounds, adjusting user, group, and other permission bits to match prompts. When the challenge changed ownership of `/flag`, used `chmod a+r /flag` to read the file.

### What I learned

Practice with symbolic mode `u=`, `g=`, `o=` and `a=` is useful. Work in small steps. Verify with `ls -l` after each change.

---

# permissions-setting-practice

type: more complex permission puzzles using `chmod` symbolic modes

## My solve

**Flag:** `pwn.college{MVpmSpTKJnE59acjPL9HgDT2QYZ.QXzETO0wSN0EzNzEzW}`

WSL terminal session excerpts:

```bash
# rounds of setting permissions to exact masks
hacker@permissions~permissions-setting-practice:~$ chmod u=rx,g=rx,o= /challenge/pwn
hacker@permissions~permissions-setting-practice:~$ chmod a=x /challenge/pwn
hacker@permissions~permissions-setting-practice:~$ chmod u=x,g=r,o=rx /challenge/pwn
hacker@permissions~permissions-setting-practice:~$ chmod u=rw,g=rx,o=wx /challenge/pwn
hacker@permissions~permissions-setting-practice:~$ chmod a+r /flag
hacker@permissions~permissions-setting-practice:~$ cat /flag
pwn.college{MVpmSpTKJnE59acjPL9HgDT2QYZ.QXzETO0wSN0EzNzEzW}
```

### My solve

Followed the prompts and used symbolic `chmod` to reach the exact permission masks for each round. When ownership and permissions allowed, added read for all to `/flag` and read it.

### What I learned

Symbolic and octal `chmod` both work. Understand which bits each symbolic token sets or clears.

---

# the-suid-bit

type: set SUID with `chmod u+s` and run a root-owned program

## My solve

**Flag:** `pwn.college{o7hBaStCTCzoaRZSdcH4ekg-lLW.QXzEjN0wSN0EzNzEzW}`

WSL terminal session:

```bash
hacker@permissions~the-suid-bit:~$ ls -l /challenge/getroot
-rwxr-xr-x 1 root root 155 Jan 14  2025 /challenge/getroot
hacker@permissions~the-suid-bit:~$ chmod u+s /challenge/getroot
hacker@permissions~the-suid-bit:~$ ls -l /challenge/getroot
-rwsr-xr-x 1 root root 155 Jan 14  2025 /challenge/getroot
hacker@permissions~the-suid-bit:~$ /challenge/getroot
SUCCESS! You have set the suid bit on this program, and it is running as root!
Here is your shell...
root@permissions~the-suid-bit:~# whoami
root
root@permissions~the-suid-bit:~# cat /flag
pwn.college{o7hBaStCTCzoaRZSdcH4ekg-lLW.QXzEjN0wSN0EzNzEzW}
```

### My solve

Set the SUID bit with `chmod u+s /challenge/getroot`. Executing the binary then runs it with root privileges and provided a root shell to read `/flag`.

### What I learned

The SUID bit allows executables to run with the file owner's privileges (often root). Setting SUID on root-owned programs can grant elevated access. Use responsibly and understand security implications.

---

## References

* `man chmod`
* `man chown`
* `man chgrp`
* `man su`
* `man mount` (general permissions context)
