# Bash Globbing and Tab Completion — Full Module Writeups

# Globbing Basics

## matching-with-asterisk
**Flag:** `pwn.college{cesz6jQkoW8ohqXSsPmezCVxWgp.QXxIDO0wSN0EzNzEzW}`

WSL terminal session:
```wsl
hacker@globbing~matching-with-:~$ cd /ch*
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{cesz6jQkoW8ohqXSsPmezCVxWgp.QXxIDO0wSN0EzNzEzW}
```

### My solve
Used the `*` wildcard to match `/challenge` with `/ch*` for `cd`. Then ran `/challenge/run` to get the flag.

### What I learned
`*` matches any sequence of characters (except leading `.` or `/`). Useful to shorten commands or match multiple files.

---

## matching-with-question-mark
**Flag:** `pwn.college{4eRrpnZdyaCm7UlNrkm5lvsdwsT.QXyIDO0wSN0EzNzEzW}`

WSL terminal session:
```wsl
hacker@globbing~matching-with-:~$ cd /?ha??enge
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{4eRrpnZdyaCm7UlNrkm5lvsdwsT.QXyIDO0wSN0EzNzEzW}
```

### My solve
Used `?` as a single-character wildcard to match each character in `/challenge`.

### What I learned
`?` matches exactly one character. Useful for precise matching when filenames differ by a few letters.

---

## bracket-globbing
**Flag:** `pwn.college{4SUAS0Gj4y7oISodgfkzfqc1SVd.QXzIDO0wSN0EzNzEzW}`

WSL terminal session:
```wsl
hacker@globbing~matching-with-:~$ /challenge/run file_[a,b,s,h]
You got it! Here is your flag!
pwn.college{4SUAS0Gj4y7oISodgfkzfqc1SVd.QXzIDO0wSN0EzNzEzW}
```

### My solve
Used `[absh]` to match one character from the set in file names.

### What I learned
`[]` allows limited wildcarding — matches any one character inside the brackets.

---

## absolute-path-bracket-globbing
**Flag:** `pwn.college{k3qK2BMGAmz8OWIn26LIawvYjWc.QX0IDO0wSN0EzNzEzW}`

WSL terminal session:
```wsl
hacker@globbing~matching-paths-with-:~$ /challenge/run /challenge/files/file_[absh]
You got it! Here is your flag!
pwn.college{k3qK2BMGAmz8OWIn26LIawvYjWc.QX0IDO0wSN0EzNzEzW}
```

### My solve
Used bracket globbing on absolute paths to match `/challenge/files/file_b`, `file_a`, `file_s`, and `file_h`.

### What I learned
Globs can be used with full paths, not just filenames.

---

## multiple-globs
**Flag:** `pwn.college{8Yq3JkluFmjh21VYhF_7ajZxgNn.0lM3kjNxwSN0EzNzEzW}`

WSL terminal session:
```wsl
hacker@globbing~multiple-globs:~$ /challenge/run *p*
You got it! Here is your flag!
pwn.college{8Yq3JkluFmjh21VYhF_7ajZxgNn.0lM3kjNxwSN0EzNzEzW}
```

### My solve
Used a single glob `*p*` to match all files containing `p`.

### What I learned
Multiple globs can be combined in one word to match more complex patterns.

---

## exclusionary-globbing
**Flag:** `pwn.college{QlXLKbkUjrYokkFiLtY9MpCJ0Lu.QX2IDO0wSN0EzNzEzW}`

WSL terminal session:
```wsl
hacker@globbing~exclusionary-globbing:~$ /challenge/run [^pwn]*
You got it! Here is your flag!
pwn.college{QlXLKbkUjrYokkFiLtY9MpCJ0Lu.QX2IDO0wSN0EzNzEzW}
```

### My solve
Used `[^pwn]*` to exclude characters `p`, `w`, or `n` in the match.

### What I learned
`[^...]` allows negation of characters within brackets.

---

# Tab Completion

## tab-completion-for-files
**Flag:** `pwn.college{Ich3E-00GgBjKs66PTBRKqp8Qjc.0FN0EzNxwSN0EzNzEzW}`

WSL terminal session:
```wsl
hacker@globbing~tab-completion:~$ cat /challenge/pwncollege​
pwn.college{Ich3E-00GgBjKs66PTBRKqp8Qjc.0FN0EzNxwSN0EzNzEzW}
```

### My solve
Used tab-completion to auto-complete the tricky filename in `/challenge`.

### What I learned
Tab-completion prevents errors and saves typing. It is essential for tricky filenames that are hard to type.

---

## multiple-options-tab-completion
**Flag:** `pwn.college{AMvtCYf05tQe0FKd3fSKP5dZOk_.0lN0EzNxwSN0EzNzEzW}`

WSL terminal session:
```wsl
hacker@globbing~multiple-options-for-tab-completion:/challenge/files$ cat ./pwncollege-flag
pwn.college{AMvtCYf05tQe0FKd3fSKP5dZOk_.0lN0EzNxwSN0EzNzEzW}
```

### My solve
Navigated `/challenge/files` with tab-completion to locate `pwncollege-flag` and cat the file.

### What I learned
When multiple files match the prefix, hitting tab twice lists all options. Helps discover files with similar names.

---

## tab-completion-on-commands
**Flag:** `pwn.college{Ytit3XF4r2schLSQ34YqRbcAy6Y.0VN0EzNxwSN0EzNzEzW}`

WSL terminal session:
```wsl
hacker@globbing~tab-completion-on-commands:~$ pwncollege-1889
Correct! Here is your flag:
pwn.college{Ytit3XF4r2schLSQ34YqRbcAy6Y.0VN0EzNxwSN0EzNzEzW}
```

### My solve
Used tab-completion for commands to auto-complete a `pwncollege` binary that gives the flag.

### What I learned
Tab completion works for both filenames and commands. It prevents mistakes and speeds up navigation.

---


