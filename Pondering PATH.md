# the-path-variable

type: run a command with an empty PATH to avoid external commands

## My solve

**Flag:** `pwn.college{0KJyOIkSd_-FFtL_0L_IX4Efk8O.QX2cDM1wSN0EzNzEzW}`

WSL terminal session:

```bash
hacker@path~the-path-variable:~$ PATH= /challenge/run
Trying to remove /flag...
/challenge/run: line 4: rm: No such file or directory
The flag is still there! I might as well give it to you!
pwn.college{0KJyOIkSd_-FFtL_0L_IX4Efk8O.QX2cDM1wSN0EzNzEzW}
```

### My solve

Cleared `PATH` before running the harness so shell builtins were used and external `rm` couldn't be found. The harness failed to delete `/flag` and printed the flag.

### What I learned

An empty `PATH` prevents execution of external commands found in directories. Useful to neutralize scripts that call external programs by name.

---

# setting-path

type: set PATH to include a directory with helper commands used by the harness

## My solve

**Flag:** `pwn.college{UGVUvrVC5XT7I6GuXGyMKXPtNPY.QX1cjM1wSN0EzNzEzW}`

WSL terminal session:

```bash
hacker@path~setting-path:~$ PATH=/challenge/more_commands /challenge/run
Invoking 'win'....
Congratulations! You properly set the flag and 'win' has launched!
pwn.college{UGVUvrVC5XT7I6GuXGyMKXPtNPY.QX1cjM1wSN0EzNzEzW}
```

### My solve

Set `PATH` to a directory provided by the challenge that contains the expected helper `win`. Running the harness caused it to locate `win` there and print the flag.

### What I learned

Temporarily overriding `PATH` changes command resolution order and can redirect a program to use alternative binaries in controlled dirs.

---

# finding-commands

type: locate a command with `which`, inspect its directory, and read associated files

## My solve

**Flag:** `pwn.college{8IGzmkgd7-BKTJ8bcuL-2xlmXCc.01NzEzNxwSN0EzNzEzW}`

WSL terminal session:

```bash
hacker@path~finding-commands:~$ which win
/challenge/paths/23931/win
hacker@path~finding-commands:~$ dir=$(dirname "$(which win)")
hacker@path~finding-commands:~$ ls -l "$dir/flag"
-rw-r--r-- 1 root root 61 Oct 10 22:52 /challenge/paths/23931/flag
hacker@path~finding-commands:~$ cat "$dir/flag"
pwn.college{8IGzmkgd7-BKTJ8bcuL-2xlmXCc.01NzEzNxwSN0EzNzEzW}
```

### My solve

Used `which` to find the absolute path of `win`, extracted its directory with `dirname`, then read the `flag` file located there.

### What I learned

`which` and `dirname` help locate related files. Many challenges hide flags near helper binaries.

---

# adding-commands

type: create a custom executable and add it to PATH to override behavior

## My solve

**Flag:** `pwn.college{smTo9tK4zJcqf9V-XXlBphz-_6I.QX2cjM1wSN0EzNzEzW}`

WSL terminal session:

```bash
hacker@path~adding-commands:~$ mkdir -p /home/hacker/mybin
cat > /home/hacker/mybin/win <<'EOF'
#!/bin/bash
read -r FLAG < /flag
echo "$FLAG"
EOF
hacker@path~adding-commands:~$ chmod +x /home/hacker/mybin/win
hacker@path~adding-commands:~$ PATH=/home/hacker/mybin /challenge/run
Invoking 'win'....
pwn.college{smTo9tK4zJcqf9V-XXlBphz-_6I.QX2cjM1wSN0EzNzEzW}
```

### My solve

Wrote a small `win` script that prints `/flag`. Placed it in `~/mybin`, set it executable, then ran the harness with `PATH` pointing to that directory so the harness executed the custom script.

### What I learned

Creating custom commands and pointing `PATH` at them allows you to intercept expected calls by a program. This is essential for binary-hijack style challenges.

---

## References

* `man bash` (command lookup and PATH behavior)
* `man which`
* `dirname` utility notes
