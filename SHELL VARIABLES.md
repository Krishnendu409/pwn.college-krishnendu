# Variables — Full Module Writeups

## Printing Variables
What the challenge asks: Print the value stored in the variable FLAG.

**Flag:** `pwn.college{4Scdz-a3FNvoLu_-WMk6pXI7ncb.QX3UTN0wSN0EzNzEzW}`
```
hacker@variables~printing-variables:~$ echo $FLAG
pwn.college{4Scdz-a3FNvoLu_-WMk6pXI7ncb.QX3UTN0wSN0EzNzEzW}
```
### My solve
Used echo $FLAG to print the variable.

### What I learned
$VAR expands to the value stored in the variable VAR.

### References
Bash variable expansion docs.

---

## Setting Variables
What the challenge asks: Set PWN to COLLEGE and print it to get the flag.

**Flag:** `pwn.college{w7XUq6S_QtKjOqLByNWF76Is6YQ.QX5UTN0wSN0EzNzEzW}`
```
hacker@variables~setting-variables:~$ PWN=COLLEGE
hacker@variables~setting-variables:~$ echo "$PWN"
COLLEGE
```
### My solve
Assigned PWN=COLLEGE and echoed it.

### What I learned
Variable assignment uses = with no spaces; $VAR is used to access it.

### References
Bash variable assignment docs.

---

## Multi-word Variables
What the challenge asks: Set PWN to "COLLEGE YEAH" including spaces.

**Flag:** `pwn.college{sv18duGLnGTKhlG8ABNegV_a50N.QXwYTN0wSN0EzNzEzW}`
```
hacker@variables~multi-word-variables:~$ PWN="COLLEGE YEAH"
hacker@variables~multi-word-variables:~$ echo "$PWN"
COLLEGE YEAH
```
### My solve
Used quotes to store multi-word values.

### What I learned
Quotes allow spaces in variable values.

### References
Bash quoting docs.

---

## Exporting Variables
What the challenge asks: Export PWN so child processes can access it; set COLLEGE locally.

**Flag:** `pwn.college{ohLOeWffAX9iyHs-BGoFrqzPfBK.QXyYTN0wSN0EzNzEzW}`
```
hacker@variables~exporting-variables:~$ export PWN=COLLEGE
hacker@variables~exporting-variables:~$ COLLEGE=PWN
hacker@variables~exporting-variables:~$ /challenge/run
CORRECT!
```
### My solve
Exported PWN and ran /challenge/run with the proper local variable COLLEGE.

### What I learned
export VAR makes the variable available to child processes.

### References
Bash export docs.

---

## Printing Exported Variables
What the challenge asks: Print all exported variables to find FLAG.

**Flag:** `pwn.college{Uef9bxsbwr03OiiAwJA1WhhfpS0.QX4UTN0wSN0EzNzEzW}`
```
hacker@variables~printing-exported-variables:~$ printenv FLAG
pwn.college{Uef9bxsbwr03OiiAwJA1WhhfpS0.QX4UTN0wSN0EzNzEzW}
```
### My solve
Used printenv FLAG to access exported variables.

### What I learned
printenv lists exported environment variables.

### References
Bash printenv docs.

---

## Storing Command Output in Variables
What the challenge asks: Store the output of /challenge/run into PWN.

**Flag:** `pwn.college{Q723MA4cfSJd7RXqQtNR2CW5dCs.QX1cDN1wSN0EzNzEzW}`
```
hacker@variables~storing-command-output:~$ PWN=$(/challenge/run)
hacker@variables~storing-command-output:~$ export PWN
hacker@variables~storing-command-output:~$ printenv PWN
pwn.college{Q723MA4cfSJd7RXqQtNR2CW5dCs.QX1cDN1wSN0EzNzEzW}
```
### My solve
Used $(command) to capture stdout into a variable.

### What I learned
Command substitution VAR=$(command) stores program output in a variable.

### References
Bash command substitution docs.

---

## Reading Input into Variables
What the challenge asks: Use read to set PWN to COLLEGE.

**Flag:** `pwn.college{w7XUq6S_QtKjOqLByNWF76Is6YQ.QX5UTN0wSN0EzNzEzW}`
```
hacker@variables~reading-input:~$ read -p "Enter value: " PWN
Enter value: COLLEGE
hacker@variables~reading-input:~$ echo $PWN
COLLEGE
```
### My solve
Used read -p to take input into a variable.

### What I learned
read VAR reads standard input into a variable; -p adds a prompt.

### References
Bash read docs.

