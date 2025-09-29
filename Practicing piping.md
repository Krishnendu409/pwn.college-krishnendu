# Redirecting Output
type what the challenge asks

## My solve
WSL terminal session:
```wsl
hacker@piping~redirecting-output:~$ echo PWN > COLLEGE
hacker@piping~redirecting-output:~$ /challenge/run > myflag
hacker@piping~redirecting-output:~$ cat myflag
pwn.college{Q6EzgvjrS7ma0gqFph0be-rzb04.QX0YTN0wSN0EzNzEzW}
```

**Flag:** `pwn.college{Q6EzgvjrS7ma0gqFph0be-rzb04.QX0YTN0wSN0EzNzEzW}`

### What I learned
- `>` redirects stdout to a file (overwrites existing content).  
- You can save program output to a file for later use.

### References
didn’t use anything

---

# Redirecting More Output
type what the challenge asks

## My solve
WSL terminal session:
```wsl
hacker@piping~redirecting-more-output:~$ /challenge/run > myflag
hacker@piping~redirecting-more-output:~$ cat myflag
pwn.college{0CNDloLG9d_zC2Ab3rJS186mH0w.QX1YTN0wSN0EzNzEzW}
```

**Flag:** `pwn.college{0CNDloLG9d_zC2Ab3rJS186mH0w.QX1YTN0wSN0EzNzEzW}`

### What I learned
- Some challenges only give flags when output is redirected.  
- Always verify with `cat` to ensure the file contains the expected result.

### References
didn’t use anything

---

# Appending Output
type what the challenge asks

## My solve
WSL terminal session:
```wsl
hacker@piping~appending-output:~$ /challenge/run > /home/hacker/the-flag
hacker@piping~appending-output:~$ /challenge/run >> /home/hacker/the-flag
hacker@piping~appending-output:~$ cat /home/hacker/the-flag
pwn.college{wIuC1lO2ZTA1q7-1MiErnFvAJtD.QX3ATO0wSN0EzNzEzW}
```

**Flag:** `pwn.college{wIuC1lO2ZTA1q7-1MiErnFvAJtD.QX3ATO0wSN0EzNzEzW}`

### What I learned
- `>>` appends output instead of overwriting like `>`.  
- Useful for combining partial outputs into one file.

### References
didn’t use anything

---

# Redirecting Errors
type what the challenge asks

## My solve
WSL terminal session:
```wsl
hacker@piping~redirecting-errors:~$ /challenge/run >myflag 2>instructions
hacker@piping~redirecting-errors:~$ cat myflag
pwn.college{gncW8Nyhwx021zZuZOD9Tek7U62.QX3YTN0wSN0EzNzEzW}
```

**Flag:** `pwn.college{gncW8Nyhwx021zZuZOD9Tek7U62.QX3YTN0wSN0EzNzEzW}`

### What I learned
- `2>` redirects stderr separately from stdout.  
- `>file 2>file2` can capture different streams.

### References
didn’t use anything

---

# Redirecting Input
type what the challenge asks

## My solve
WSL terminal session:
```wsl
hacker@piping~redirecting-input:~$ echo COLLEGE > PWN
hacker@piping~redirecting-input:~$ /challenge/run < PWN
pwn.college{cdwoL5YhDa8zddM-oIgsgDWrFiZ.QXwcTN0wSN0EzNzEzW}
```

**Flag:** `pwn.college{cdwoL5YhDa8zddM-oIgsgDWrFiZ.QXwcTN0wSN0EzNzEzW}`

### What I learned
- `< file` redirects a file into stdin for a program.  
- Saves effort instead of typing interactively.

### References
didn’t use anything

---

# Grepping Stored Results
type what the challenge asks

## My solve
WSL terminal session:
```wsl
hacker@piping~grepping-stored-results:~$ /challenge/run > /tmp/data.txt
hacker@piping~grepping-stored-results:~$ grep "pwn.college" /tmp/data.txt
pwn.college{gLqi3tLxUZfs-Fl_wKPYofumrI8.QX4EDO0wSN0EzNzEzW}
```

**Flag:** `pwn.college{gLqi3tLxUZfs-Fl_wKPYofumrI8.QX4EDO0wSN0EzNzEzW}`

### What I learned
- You can grep inside a file to extract relevant lines.  
- Combining `>` and `grep` is useful for large outputs.

### References
didn’t use anything

---

# Grepping Live Output
type what the challenge asks

## My solve
WSL terminal session:
```wsl
hacker@piping~grepping-live-output:~$ /challenge/run | grep pwn.college
pwn.college{A9nO4AzGgx0IkatTPrHsXi6SQG1.QX5EDO0wSN0EzNzEzW}
```

**Flag:** `pwn.college{A9nO4AzGgx0IkatTPrHsXi6SQG1.QX5EDO0wSN0EzNzEzW}`

### What I learned
- `|` pipes stdout of one program into another.  
- Faster than redirecting to a file and grepping.

### References
didn’t use anything

---

# Grepping Errors
type what the challenge asks

## My solve
WSL terminal session:
```wsl
hacker@piping~grepping-errors:~$ /challenge/run 2>&1 | grep pwn.college
pwn.college{QBbBzfN-L70Cacjg5-BPL-XcZcC.QX1ATO0wSN0EzNzEzW}
```

**Flag:** `pwn.college{QBbBzfN-L70Cacjg5-BPL-XcZcC.QX1ATO0wSN0EzNzEzW}`

### What I learned
- `2>&1` merges stderr into stdout.  
- Allows piping error messages into another command like `grep`.

### References
didn’t use anything

---

# Writing to Multiple Programs
type what the challenge asks

## My solve
WSL terminal session:
```wsl
hacker@piping~writing-to-multiple-programs:~$ /challenge/hack | tee >( /challenge/the ) >( /challenge/planet )
pwn.college{snzOsMISgdvaDpcPkEaLYmW-56n.QXwgDN1wSN0EzNzEzW}
```

**Flag:** `pwn.college{snzOsMISgdvaDpcPkEaLYmW-56n.QXwgDN1wSN0EzNzEzW}`

### What I learned
- `tee` writes output to multiple places.  
- Process substitution `>(cmd)` lets you route one program’s output into several others simultaneously.

### References
didn’t use anything
