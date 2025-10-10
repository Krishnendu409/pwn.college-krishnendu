# chaining-with-semicolons

type: chain commands with `;`

## My solve

**Flag:** `pwn.college{EYtRu8cWuUwCcXRlj4nPDoM5GXT.QX1UDO0wSN0EzNzEzW}`

WSL terminal session:

```bash
hacker@chaining~chaining-with-semicolons:~$ /challenge/pwn; /challenge/college
Yes! You chained /challenge/pwn and /challenge/college! Here is your flag:
pwn.college{EYtRu8cWuUwCcXRlj4nPDoM5GXT.QX1UDO0wSN0EzNzEzW}
```

### My solve

Ran two commands separated by `;` so both executed sequentially regardless of exit status.

### What I learned

`;` runs commands sequentially without checking success.

---

# building-on-success

type: chain commands with `&&` to require success

## My solve

**Flag:** `pwn.college{ET4gr0cwgViuFn83s1t_limZvdS.0lM0MDOxwSN0EzNzEzW}`

WSL terminal session:

```bash
hacker@chaining~building-on-success:~$ /challenge/first-success && /challenge/second
Nice chaining! Flag: pwn.college{ET4gr0cwgViuFn83s1t_limZvdS.0lM0MDOxwSN0EzNzEzW}
```

### My solve

Used `&&` so the second command ran only after the first succeeded (exit code 0).

### What I learned

`&&` enforces dependency on prior command success.

---

# handling-failure

type: chain with `||` to run on failure

## My solve

**Flag:** `pwn.college{o0SnQIoEHAEa5L79DVq4ojlrCch.01M0MDOxwSN0EzNzEzW}`

WSL terminal session:

```bash
hacker@chaining~handling-failure:~$ /challenge/first-failure || /challenge/second

Nice chaining! Flag: pwn.college{o0SnQIoEHAEa5L79DVq4ojlrCch.01M0MDOxwSN0EzNzEzW}
```

### My solve

Used `||` to run a fallback command when the first failed (nonzero exit).

### What I learned

`||` is for fallback logic when a command fails.

---

# your-first-shell-script

type: write a basic shell script

## My solve

**Flag:** `pwn.college{kFDj720zDvKuO7RfYAdiQ0F6jly.QXxcDO0wSN0EzNzEzW}`

WSL terminal session:

```bash
hacker@chaining~your-first-shell-script:~$ cat > x.sh <<'EOF'
/challenge/pwn
/challenge/college
EOF
hacker@chaining~your-first-shell-script:~$ bash x.sh
Great job, you've written your first shell script! Here is your flag:
pwn.college{kFDj720zDvKuO7RfYAdiQ0F6jly.QXxcDO0wSN0EzNzEzW}
```

### My solve

Wrote `x.sh` containing two commands and executed it with `bash x.sh`.

### What I learned

Scripts automate sequences of commands.

---

# redirecting-script-output

type: pipe script output into another command

## My solve

**Flag:** `pwn.college{MBMnqomjGswQoqFMHV14zUbT_t5.QX4ETO0wSN0EzNzEzW}`

WSL terminal session:

```bash
hacker@chaining~redirecting-script-output:~$ cat > x.sh <<'EOF'
/challenge/pwn
/challenge/college
EOF

bash x.sh | /challenge/solve
Correct! Here is your flag:
pwn.college{MBMnqomjGswQoqFMHV14zUbT_t5.QX4ETO0wSN0EzNzEzW}
```

### My solve

Piped script stdout into another program to validate output.

### What I learned

Pipes forward stdout to another process for processing.

---

# executable-shell-scripts

type: make script executable and run directly

## My solve

**Flag:** `pwn.college{UyC776XP4652KUyN1vVtid-MvmU.QX0cjM1wSN0EzNzEzW}`

WSL terminal session:

```bash
hacker@chaining~executable-shell-scripts:~$ cat > x.sh <<'EOF'
/challenge/solve
EOF
hacker@chaining~executable-shell-scripts:~$ chmod +x x.sh

./x.sh
Congratulations on your shell script execution! Your flag:
pwn.college{UyC776XP4652KUyN1vVtid-MvmU.QX0cjM1wSN0EzNzEzW}
```

### My solve

Made the script executable and ran it directly.

### What I learned

Executable bit allows running scripts without `bash` prefix when compatible.

---

# understanding-shebangs

type: add shebang and run script under challenge harness

## My solve

**Flag:** `pwn.college{cXGFN8sKh0lFm6_MVlXWnX1x3dQ.0VOzMDOxwSN0EzNzEzW}`

WSL terminal session:

```bash
hacker@chaining~understanding-shebangs:~$ cat > /home/hacker/solve.sh <<'EOF'
#!/bin/bash
echo "hack the planet"
EOF
chmod +x /home/hacker/solve.sh
hacker@chaining~understanding-shebangs:~$ /challenge/run
Testing your script...
Perfect! Your flag:
Flag: pwn.college{cXGFN8sKh0lFm6_MVlXWnX1x3dQ.0VOzMDOxwSN0EzNzEzW}
```

### My solve

Used `#!/bin/bash` as the interpreter and let the harness execute the script.

### What I learned

Shebang specifies the interpreter used when executing a script file.

---

# scripting-with-arguments

type: handle positional parameters in scripts

## My solve

**Flag:** `pwn.college{kjF-Cf8hQ9h8NQyxM0NWQgpXxF6.0VNzMDOxwSN0EzNzEzW}`

WSL terminal session:

```bash
hacker@chaining~scripting-with-arguments:~$ cat > /home/hacker/solve.sh <<'EOF'
#!/bin/bash
echo "$2 $1"
EOF

chmod +x /home/hacker/solve.sh

# quick manual test
/home/hacker/solve.sh pwn college

# then run the challenge check
/challenge/run
college pwn
Correct! Your script properly reversed the arguments.
Here's your flag:
pwn.college{kjF-Cf8hQ9h8NQyxM0NWQgpXxF6.0VNzMDOxwSN0EzNzEzW}
```

### My solve

Used `$1` and `$2` to reverse arguments and print them.

### What I learned

Positional parameters provide simple input to scripts.

---

# scripting-with-conditionals

type: basic if condition in a script

## My solve

**Flag:** `pwn.college{gS0laamyKpe0O4mLLHu9EciS_aF.0lNzMDOxwSN0EzNzEzW}`

WSL terminal session:

```bash
hacker@chaining~scripting-with-conditionals:~$ cat > /home/hacker/solve.sh <<'EOF'
#!/bin/bash
if [ "$1" = "pwn" ]
then
  echo "college"
fi
EOF

chmod +x /home/hacker/solve.sh

# test
/home/hacker/solve.sh pwn

# then verify
/challenge/run
college
Correct! Your script properly handles all the conditions.
Here's your flag:
pwn.college{gS0laamyKpe0O4mLLHu9EciS_aF.0lNzMDOxwSN0EzNzEzW}
```

### My solve

Wrote an `if` that prints when the argument matches the target.

### What I learned

Use `if [ "..." = "..." ]` for string tests in shell.

---

# scripting-with-default-cases

type: add if/else fallback behavior

## My solve

**Flag:** `pwn.college{4JQRBLEUMZAmPn44xnyGYn3A753.01NzMDOxwSN0EzNzEzW}`

WSL terminal session:

```bash
hacker@chaining~scripting-with-default-cases:~$ cat > /home/hacker/solve.sh <<'EOF'
#!/bin/bash
if [ "$1" = "pwn" ]; then
  echo "college"
else
  echo "nope"
fi
EOF

chmod +x /home/hacker/solve.sh
/home/hacker/solve.sh pwn
/challenge/run
college
Correct! Your script properly handles the if/else conditions.
Here's your flag:
pwn.college{4JQRBLEUMZAmPn44xnyGYn3A753.01NzMDOxwSN0EzNzEzW}
```

### My solve

Provided a fallback `else` branch for non-matching inputs.

### What I learned

`else` ensures a default response when conditions fail.

---

# scripting-with-multiple-conditions

type: use `elif` for multiple branches

## My solve

**Flag:** `pwn.college{g0rwqASuShKdGBuenm0ue2twq5E.0FOzMDOxwSN0EzNzEzW}`

WSL terminal session:

```bash
hacker@chaining~scripting-with-multiple-conditions:~$ cat > /home/hacker/solve.sh <<'EOF'
#!/bin/bash
if [ "$1" = "hack" ]; then
  echo "the planet"
elif [ "$1" = "pwn" ]; then
  echo "college"
elif [ "$1" = "learn" ]; then
  echo "linux"
else
  echo "unknown"
fi
EOF

chmod +x /home/hacker/solve.sh
hacker@chaining~scripting-with-multiple-conditions:~$ /home/hacker/solve.sh hack
/home/hacker/solve.sh pwn
/home/hacker/solve.sh learn
/home/hacker/solve.sh foo
the planet
college
linux
unknown
hacker@chaining~scripting-with-multiple-conditions:~$ /challenge/run
Correct! Your script properly handles all the conditions with elif.
Here's your flag:
pwn.college{g0rwqASuShKdGBuenm0ue2twq5E.0FOzMDOxwSN0EzNzEzW}
```

### My solve

Implemented `elif` branches and tested multiple inputs.

### What I learned

`elif` simplifies multi-way logic.

---

# reading-shell-scripts

type: inspect a setuid shell script to learn the required input

## My solve

**Flag:** `pwn.college{QFsHLKbAhlFw9W8P8o7woCok5Su.0lMwgDOxwSN0EzNzEzW}`

WSL terminal session:

```bash
hacker@chaining~reading-shell-scripts:~$ ls -l /challenge/run && file /challenge/run
-rwsr-xr-x 1 root root 198 Aug 24 19:04 /challenge/run
/challenge/run: setuid a /opt/pwn.college/bash script, ASCII text executable
hacker@chaining~reading-shell-scripts:~$ cat /challenge/run
#!/opt/pwn.college/bash

read GUESS
if [ "$GUESS" == "hack the PLANET" ]
then
        echo "CORRECT! Your flag:"
        cat /flag
else
        echo "Read the /challenge/run file to figure out the correct password!"
fi
hacker@chaining~reading-shell-scripts:~$ printf 'hack the PLANET\n' | /challenge/run
CORRECT! Your flag:
pwn.college{QFsHLKbAhlFw9W8P8o7woCok5Su.0lMwgDOxwSN0EzNzEzW}
```

### My solve

Read the setuid script to discover the exact input string. Piped that input into the program to produce the flag.

### What I learned

Reading scripts reveals expected input. Use `printf` to supply exact strings to programs.

---

## References

* `man bash`
* `Advanced Bash-Scripting Guide`
* `POSIX sh`
