# Learning From Documentation — Full Module Writeups

# Learning From Documentation

## learning-from-documentation
**Flag:** `pwn.college{UTc92aXzc7wMQJDJwWLL8FjP1yx.QX0ITO0wSN0EzNzEzW}`

WSL terminal session:
```wsl
hacker@man~learning-from-documentation:~$ /challenge/challenge --giveflag
Correct argument! Here is your flag:
pwn.college{UTc92aXzc7wMQJDJwWLL8FjP1yx.QX0ITO0wSN0EzNzEzW}
```

### My solve
The challenge documentation explicitly instructed using `--giveflag`. Running `/challenge/challenge --giveflag` returned the flag.

### What I learned
How simple command-line arguments are documented and used; using documentation to discover required flags.

### References
Challenge description / on-board docs.

---

## learning-complex-usage
**Flag:** `pwn.college{EPZyYIYCl4nE0EfwApIQuD_ueHL.QX1ITO0wSN0EzNzEzW}`

WSL terminal session:
```wsl
hacker@man~learning-complex-usage:~$ /challenge/challenge --printfile ~/not-the-flag
Correct argument! Here is the /home/hacker/not-the-flag file:
pwn.college{EPZyYIYCl4nE0EfwApIQuD_ueHL.QX1ITO0wSN0EzNzEzW}
```

### My solve
Used the documented `--printfile` option with the path `~/not-the-flag` to print the target file's contents.

### What I learned
Some options themselves take arguments (e.g., `--printfile <path>`); read docs to know what type of argument to supply.

### References
Challenge docs.

---

## reading-manuals
**Flag:** `pwn.college{44QMvvlSIdMdK4yaUMARf8WdpnC.QX0EDO0wSN0EzNzEzW}`

WSL terminal session:
```wsl
hacker@man~reading-manuals:~$ man challenge
hacker@man~reading-manuals:~$ /challenge/challenge --vvlddy 444
Correct usage! Your flag: pwn.college{44QMvvlSIdMdK4yaUMARf8WdpnC.QX0EDO0wSN0EzNzEzW}
```

### My solve
Read the `challenge` manpage to discover a hidden/less-obvious option. Invoking with `--vvlddy 444` returned the flag.

### What I learned
How to use `man` pages to find hidden or uncommon options and the basic manpage layout (NAME, SYNOPSIS, DESCRIPTION).

### References
`man` pages (challenge manpage).

---

## searching-manuals
**Flag:** `pwn.college{EQK9O1SG9BBH5p55alrfN_TeqXY.QX1EDO0wSN0EzNzEzW}`

WSL terminal session:
```wsl
hacker@man~searching-manuals:~$ man challenge
hacker@man~searching-manuals:~$ /challenge/challenge --vpqijf
Initializing...
Correct usage! Your flag: pwn.college{EQK9O1SG9BBH5p55alrfN_TeqXY.QX1EDO0wSN0EzNzEzW}
```

### My solve
Searched inside the manpage (using man’s interactive search, e.g., `/` then `n`) to locate the `--vpqijf` option and invoked it to get the flag.

### What I learned
Using man page searching (`/`, `n`, `N`) to find specific options or strings inside manuals.

### References
`man` (search features).

---

## searching-for-manuals
**Flag:** `pwn.college{YBpnqXdTabtW3Colq25P7UMFVCu.QX2EDO0wSN0EzNzEzW}`

WSL terminal session:
```wsl
hacker@man~searching-for-manuals:~$ man -K challenge/challenge
/challenge/challenge
hacker@man~searching-for-manuals:~$ /challenge/challenge --pnqdab 325
Correct usage! Your flag: pwn.college{YBpnqXdTabtW3Colq25P7UMFVCu.QX2EDO0wSN0EzNzEzW}
```

### My solve
The challenge manpage was randomized; I used `man -K` (search the man-db for content) to locate the correct man entry and then used the revealed option to get the flag.

### What I learned
`man -K` can search installed manpage content when names are unpredictable; useful for locating buried docs.

### References
`man` documentation (`-K` search).

---

## helpful-programs
**Flag:** `pwn.college{oMKBqZiUcA375uy0T2SmV_zgOjH.QX3IDO0wSN0EzNzEzW}`

WSL terminal session:
```wsl
hacker@man~helpful-programs:~$ /challenge/challenge --help
usage: a challenge to make you ask for help [-h] [--fortune] [-v] [-g GIVE_THE_FLAG] [-p]

optional arguments:
  -h, --help            show this help message and exit
  --fortune             read your fortune
  -v, --version         get the version number
  -g GIVE_THE_FLAG, --give-the-flag GIVE_THE_FLAG
                        get the flag, if given the correct value
  -p, --print-value     print the value that will cause the -g option to give you the flag
hacker@man~helpful-programs:~$ /challenge/challenge -p
The secret value is: 375
hacker@man~helpful-programs:~$ /challenge/challenge -g 375
Correct usage! Your flag: pwn.college{oMKBqZiUcA375uy0T2SmV_zgOjH.QX3IDO0wSN0EzNzEzW}
```

### My solve
Used `--help` to discover available options; `-p` printed the secret value (375) required by `-g`, and `-g 375` produced the flag.

### What I learned
`--help` is a quick way to discover usage and option semantics when a manpage is absent.

### References
Program `--help` output.

---

## help-for-builtins
**Flag:** `pwn.college{0Eo06yGAAJNBhWlciFhGZaiR_M-.QX0ETO0wSN0EzNzEzW}`

WSL terminal session:
```wsl
hacker@man~help-for-builtins:~$ help challenge
challenge: challenge [--fortune] [--version] [--secret SECRET]
    This builtin command will read you the flag, given the right arguments!

    Options:
      --fortune         display a fortune
      --version         display the version
      --secret VALUE    prints the flag, if VALUE is correct

    You must be sure to provide the right value to --secret. That value is "0Eo06yGA".
hacker@man~help-for-builtins:~$ challenge --secret 0Eo06yGA
Correct! Here is your flag!
pwn.college{0Eo06yGAAJNBhWlciFhGZaiR_M-.QX0ETO0wSN0EzNzEzW}
```

### My solve
Used the shell builtin `help` to reveal the `--secret` option and its required value; invoked the builtin to obtain the flag.

### What I learned
Difference between external programs (with manpages or `--help`) and shell builtins (use `help`); builtins are handled inside the shell.

### References
Shell `help` builtin; challenge notes.

---


