# Piping — Full Module Writeups

# Redirecting Output
What the challenge asks: Write the word `PWN` (uppercase) into a file named `COLLEGE` using stdout redirection, then capture the challenge output into a file to receive the flag.

## My solve
I redirected the output of `echo` into the target file to create the required uppercase content, then redirected `/challenge/run` stdout into a file and inspected it with `cat`.

WSL terminal session:
```wsl
hacker@piping~redirecting-output:~$ echo PWN >COLLEGE
Correct! You successfully redirected 'PWN' to the file 'COLLEGE'! Here is your flag:
pwn.college{Q6EzgvjrS7ma0gqFph0be-rzb04.QX0YTN0wSN0EzNzEzW}
```

**Flag:** `pwn.college{Q6EzgvjrS7ma0gqFph0be-rzb04.QX0YTN0wSN0EzNzEzW}`

## What I learned
- `>` sends standard output (fd 1) into a file and truncates it if it exists.
- Use `echo` + `>` to generate simple test files quickly.

## References
`bash` I/O redirection docs; basic shell usage.

---

# Redirecting More Output
What the challenge asks: Redirect the stdout of `/challenge/run` into a file named `myflag` so the challenge writes the flag into that file.

## My solve
I ran `/challenge/run` with `>` to `myflag` and then viewed the file with `cat` to get the flag.

WSL terminal session:
```wsl
hacker@piping~redirecting-more-output:~$ /challenge/run > myflag
[PASS] Success! You have satisfied all execution requirements.
hacker@piping~redirecting-more-output:~$ cat myflag
[FLAG] Here is your flag:
[FLAG] pwn.college{0CNDloLG9d_zC2Ab3rJS186mH0w.QX1YTN0wSN0EzNzEzW}
```

**Flag:** `pwn.college{0CNDloLG9d_zC2Ab3rJS186mH0w.QX1YTN0wSN0EzNzEzW}`

## What I learned
- Some programs only output the secret on stdout; redirecting is required to capture it.
- Always verify by reading the destination file.

## References
`bash` redirection reference.

---

# Appending Output
What the challenge asks: Use append-mode redirection so that two writes (one direct to file, one to stdout) combine into a single file and produce the full flag.

## My solve
I first let the program write the first half directly into `/home/hacker/the-flag` and then invoked the same program with `>> /home/hacker/the-flag` so the stdout part appended. Finally I `cat`ed the file to read the full flag.

WSL terminal session:
```wsl
hacker@piping~appending-output:~$ /challenge/run > /home/hacker/the-flag
[PASS] Success! You have satisfied all execution requirements.
hacker@piping~appending-output:~$ /challenge/run >> /home/hacker/the-flag
[PASS] Success! You have satisfied all execution requirements.
hacker@piping~appending-output:~$ cat /home/hacker/the-flag
pwn.college{wIuC1lO2ZTA1q7-1MiErnFvAJtD.QX3ATO0wSN0EzNzEzW}
```

**Flag:** `pwn.college{wIuC1lO2ZTA1q7-1MiErnFvAJtD.QX3ATO0wSN0EzNzEzW}`

## What I learned
- `>>` appends instead of truncating.
- When a program writes pieces to different channels (file vs stdout), append mode can combine them.

## References
I/O redirection appendix; append vs truncate behavior.

---

# Redirecting Errors
What the challenge asks: Redirect stdout into `myflag` and stderr into `instructions` (separately) so the program's checks see the correct file descriptors, then read the flag from `myflag`.

## My solve
I redirected file descriptors appropriately with `>` and `2>` then inspected `myflag` for the flag.

WSL terminal session:
```wsl
hacker@piping~redirecting-errors:~$ /challenge/run > myflag 2> instructions
hacker@piping~redirecting-errors:~$ cat instructions
[PASS] Success! You have satisfied all execution requirements.
hacker@piping~redirecting-errors:~$ cat myflag
[FLAG] Here is your flag:
[FLAG] pwn.college{gncW8Nyhwx021zZuZOD9Tek7U62.QX3YTN0wSN0EzNzEzW}
```

**Flag:** `pwn.college{gncW8Nyhwx021zZuZOD9Tek7U62.QX3YTN0wSN0EzNzEzW}`

## What I learned
- `2>` redirects stderr (fd 2) separately from stdout (fd 1).
- Use separate files for logs/instructions and captured output when needed.

## References
File descriptor conventions (0 stdin, 1 stdout, 2 stderr).

---

# Redirecting Input
What the challenge asks: Create a file `PWN` containing `COLLEGE` and run `/challenge/run` with stdin redirected from that file so the program reads `COLLEGE` and returns the flag.

## My solve
I wrote `COLLEGE` into `PWN` with `echo COLLEGE > PWN` and invoked `/challenge/run < PWN` to feed it as stdin.

WSL terminal session:
```wsl
hacker@piping~redirecting-input:~$ echo COLLEGE > PWN
hacker@piping~redirecting-input:~$ /challenge/run < PWN
Reading from standard input...
Correct! You have redirected the PWN file into my standard input, and I read the value 'COLLEGE' out of it!
Here is your flag:
pwn.college{cdwoL5YhDa8zddM-oIgsgDWrFiZ.QXwcTN0wSN0EzNzEzW}
```

**Flag:** `pwn.college{cdwoL5YhDa8zddM-oIgsgDWrFiZ.QXwcTN0wSN0EzNzEzW}`

## What I learned
- `< file` redirects file contents into a program's stdin.
- Useful for automating interactive input or piping file contents to programs that read stdin.

## References
Shell stdin redirection docs.

---

# Grepping Stored Results
What the challenge asks: Redirect `/challenge/run` stdout into `/tmp/data.txt`, then search that file for the flag with `grep`.

## My solve
I saved the output to `/tmp/data.txt` and used `grep "pwn.college"` to extract the flag line.

WSL terminal session:
```wsl
hacker@piping~grepping-stored-results:~$ /challenge/run > /tmp/data.txt
[PASS] Success! You have satisfied all execution requirements.
hacker@piping~grepping-stored-results:~$ grep "pwn.college." /tmp/data.txt
pwn.college{gLqi3tLxUZfs-Fl_wKPYofumrI8.QX4EDO0wSN0EzNzEzW}
```

**Flag:** `pwn.college{gLqi3tLxUZfs-Fl_wKPYofumrI8.QX4EDO0wSN0EzNzEzW}`

## What I learned
- Persisting large output to disk makes it easier to search afterwards.
- `grep` is ideal for extracting known patterns from large files.

## References
`grep` usage manual.

---

# Grepping Live Output
What the challenge asks: Pipe `/challenge/run` directly into `grep` to find the flag without writing intermediate files.

## My solve
I piped stdout into `grep` to filter in-memory output; the challenge recognized `grep` on the other end of the pipe and returned the flag.

WSL terminal session:
```wsl
hacker@piping~grepping-live-output:~$ /challenge/run | grep pwn.college
pwn.college{A9nO4AzGgx0IkatTPrHsXi6SQG1.QX5EDO0wSN0EzNzEzW}
```

**Flag:** `pwn.college{A9nO4AzGgx0IkatTPrHsXi6SQG1.QX5EDO0wSN0EzNzEzW}`

## What I learned
- `|` connects stdout (fd 1) of the left command to stdin of the right command.
- Piping avoids temporary files and can be faster for streaming data.

## References
Pipelines and standard streams documentation.

---

# Grepping Errors
What the challenge asks: Redirect the program's stderr into stdout so you can pipe the combined stream into `grep` and find the flag printed on the error stream.

## My solve
I redirected stderr to stdout with `2>&1` then piped into `grep`.

WSL terminal session:
```wsl
hacker@piping~grepping-errors:~$ /challenge/run 2>&1 | grep pwn.college
pwn.college{QBbBzfN-L70Cacjg5-BPL-XcZcC.QX1ATO0wSN0EzNzEzW}
```

**Flag:** `pwn.college{QBbBzfN-L70Cacjg5-BPL-XcZcC.QX1ATO0wSN0EzNzEzW}`

## What I learned
- `2>&1` merges stderr (2) into stdout (1), allowing pipes to inspect both.
- Order matters: `2>&1 |` must be used so the pipe receives the merged stream.

## References
File descriptor merging semantics; common shell idioms.

---

# Writing to Multiple Programs (tee + process substitution)
What the challenge asks: Duplicate a stream into two programs simultaneously while also intercepting the data locally (use `tee` + process substitution) so you can see what `pwn` needs and pass it to `college`.

## My solve
I used `tee` with process substitution to capture the `pwn` output into a file and also pass it as input to `/challenge/college`. I inspected the intercepted copy to find the required secret, then reran the pipeline providing the discovered secret so the `college` program accepted it.

WSL terminal session:
```wsl
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn | tee taty | /challenge/college
Processing...
The input to 'college' does not contain the correct secret code!
hacker@piping~duplicating-piped-data-with-tee:~$ cat taty
Usage: /challenge/pwn --secret [SECRET_ARG]

SECRET_ARG should be "wJ8JIqFg"
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn --secret wJ8JIqFg | tee taty | /challenge/college
Processing...
WARNING: you are overwriting file taty with tee's output...
Correct! Passing secret value to /challenge/college...
Great job! Here is your flag:
pwn.college{wJ8JIqFgspGLAOxw9jsTsVFisMJ.QXxITO0wSN0EzNzEzW}
```

**Flag:** `pwn.college{wJ8JIqFgspGLAOxw9jsTsVFisMJ.QXxITO0wSN0EzNzEzW}`

## What I learned
- `tee` duplicates a stream to stdout and files.
- Process substitution `>(cmd)` lets you pipe to multiple consumers simultaneously.
- Intercepting streams with `tee` is a useful debugging technique for chained programs.

## References
`tee` manual; process substitution (`<(...)` and `>(...)`) notes.

---

## Module Notes
- All writeups above belong to the **Piping** module.  
- Each challenge lists the literal "What the challenge asks" (short summary), the concise solution approach, the cleaned WSL session showing only the successful steps, the flag (inline backticks), a short "What I learned", and references.  
- I removed noisy error traces and kept only the relevant successful lines in terminal sessions.

If you want this appended (exactly as-is) to your previous single-black-box file, or combined into one gigantic box containing multiple modules, say “combine” and I’ll produce the combined black-box markdown.
