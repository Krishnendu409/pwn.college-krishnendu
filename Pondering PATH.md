# the-path-variable

type: run a command with an empty PATH to prevent external commands from running

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

Cleared `PATH` before launching the harness. The script attempted to call `rm` but no external `rm` was found and the harness failed to delete `/flag`, then printed the flag.

### What I learned

An empty `PATH` disables lookup of external commands. This neutralizes scripts that call external binaries by name.

---

# setting-path

type: set PATH to a provided directory so the harness uses the intended helper

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

Temporarily pointed `PATH` at `/challenge/more_commands` so the harness found the expected `win` helper and executed it.

### What I learned

Overriding `PATH` lets you choose which binaries a script will run. Use it to control execution in a sandboxed environment.

---

# finding-commands

type: locate a binary with `which`, inspect its directory, and read nearby files

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

Used `which` to find the absolute path of `win`, extracted its directory with `dirname`, then read the `flag` file located in that directory.

### What I learned

`which` and `dirname` are useful to locate helper binaries and nearby resources. Flags are often colocated with helper scripts.

---

# adding-commands

type: add a custom command to a directory and point PATH at it

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

Created a small `win` wrapper that reads and prints `/flag`. Made it executable and ran the harness with `PATH` set to include that directory so the harness executed the custom `win`.

### What I learned

You can supply your own binaries/scripts and force a program to execute them by placing them earlier in `PATH`.

---

# hijacking-commands

type: override dangerous commands by placing a fake in your `PATH` to intercept calls

## My solve

**Flag:** `pwn.college{MGYl7_XMDIdaVaeTm58Rz-VXkml.QX3cjM1wSN0EzNzEzW}`

WSL terminal session:

```bash
hacker@path~hijacking-commands:~$ mkdir -p ~/mybin
cat > ~/mybin/rm <<'EOF'
#!/bin/bash
for f in "$@"; do
  [ -e "$f" ] && cat "$f"
done
exit 1
EOF
chmod +x ~/mybin/rm
export PATH="$HOME/mybin:$PATH"
# run the challenge; your fake rm will be used
/challenge/run
Trying to remove /flag...
Found 'rm' command at /home/hacker/mybin/rm. Executing!
pwn.college{MGYl7_XMDIdaVaeTm58Rz-VXkml.QX3cjM1wSN0EzNzEzW}
```

### My solve

Wrote a fake `rm` that cats files instead of removing them. Prepending `~/mybin` to `PATH` ensured the harness used the fake `rm`, which revealed the flag.

### What I learned

Hijacking commonly used commands in `PATH` can subvert scripts. Always validate `PATH` in untrusted environments and avoid trusting external command names.

---

## References

* `man bash` (PATH lookup)
* `which` and `dirname` utilities
* Basics of command hijacking and sandbox hardening
