# processes

## listing-processes

**Flag:** `pwn.college{AaiDRQGeGwh6Hp8_QTSQrZJagKt.QX4MDO0wSN0EzNzEzW}`

WSL terminal session:

```bash
hacker@processes~listing-processes:~$ ps -efww | grep /challenge
root         132       1  0 16:32 ?        00:00:00 /challenge/30675-run-32517
hacker       153     143  0 16:33 pts/0    00:00:00 grep --color=auto /challenge
hacker@processes~listing-processes:~$ /challenge/30675-run-32517
Yahaha, you found me! Here is your flag:
pwn.college{AaiDRQGeGwh6Hp8_QTSQrZJagKt.QX4MDO0wSN0EzNzEzW}
Now I will sleep for a while (so that you could find me with 'ps').
```

### My solve

I listed processes with `ps -efww | grep /challenge` to locate the running challenge binary and then ran the discovered `/challenge/30675-run-32517` to obtain the flag.

### What I learned

Use wide `ps` output and grep to find processes by command path. Some challenge binaries run with generated names; run them directly to trigger their behavior.

---

## killing-processes

**Flag:** `pwn.college{oR0y6xZh_TDytOay512cQHkrGzC.QXyQDO0wSN0EzNzEzW}`

WSL terminal session:

```bash
hacker@processes~killing-processes:~$ pid=$(ps -ef | grep dont_run | grep -v grep | awk '{print $2}')
kill $pid
/challenge/run
Great job! Here is your payment:
pwn.college{oR0y6xZh_TDytOay512cQHkrGzC.QXyQDO0wSN0EzNzEzW}
```

### My solve

Found the PID of the target process using `ps` piped into `awk` and then killed it with `kill $pid`. After terminating the interfering process, I ran `/challenge/run` to get the flag.

### What I learned

Combine `ps`, `grep`, and `awk` to extract PIDs. `kill` followed by PID terminates processes so dependent challenges succeed.

---

## interrupting-processes

**Flag:** `pwn.college{8V6GXNSncGs8bUwC3qtTDjt2yb1.QXzQDO0wSN0EzNzEzW}`

WSL terminal session:

```bash
hacker@processes~interrupting-processes:~$ /challenge/run
I could give you the flag... but I won't, until this process exits. Remember,
you can force me to exit with Ctrl-C. Try it now!
^C
Good job! You have used Ctrl-C to interrupt this process! Here is your flag:
pwn.college{8V6GXNSncGs8bUwC3qtTDjt2yb1.QXzQDO0wSN0EzNzEzW}
```

### My solve

Started the program and sent an interrupt with Ctrl-C when prompted. That caused the program to exit and print the flag.

### What I learned

Ctrl-C sends SIGINT to the foreground process, which can be used to interrupt programs that wait for exit events.

---

## detecting-other-copies

**Flag:** `pwn.college{MB4jyDsW2c3ZLY_05azXoiPCMFj.QX1QDO0wSN0EzNzEzW}`

WSL terminal session:

```bash
# program checks for another copy of itself in this terminal
UID          PID    PPID  C STIME TTY          TIME CMD
root         154     137  0 17:14 pts/1    00:00:00 bash /challenge/run
root         180     137  0 17:15 pts/1    00:00:00 bash /challenge/run
root         182     180  0 17:15 pts/1    00:00:00 ps -f

Yay, I found another version of me! Here is the flag:
pwn.college{MB4jyDsW2c3ZLY_05azXoiPCMFj.QX1QDO0wSN0EzNzEzW}
```

### My solve

Launched multiple instances of the challenge in the same terminal so the program's self-check for existing copies succeeded and it printed the flag.

### What I learned

Some challenges require multiple concurrent processes. Launching the same binary twice in the same terminal can satisfy such checks.

---

## resuming-processes

**Flag:** `pwn.college{MVksfeWG-A1BMOa-e3EXTfxuphC.QX2QDO0wSN0EzNzEzW}`

WSL terminal session:

```bash
hacker@processes~resuming-processes:~$ /challenge/run
Let's practice resuming processes! Suspend me with Ctrl-Z, then resume me with
the 'fg' command! Or just press Enter to quit me!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~resuming-processes:~$ fg
/challenge/run
I'm back! Here's your flag:
pwn.college{MVksfeWG-A1BMOa-e3EXTfxuphC.QX2QDO0wSN0EzNzEzW}
Don't forget to press Enter to quit me!
```

### My solve

Suspended the process with Ctrl-Z then used `fg` to resume it in the foreground. After resuming, followed the prompt to exit and got the flag.

### What I learned

Ctrl-Z sends SIGTSTP to suspend. `fg` resumes a job in the foreground. Job control is essential for interactive process challenges.

---

## backgrounding-processes

**Flag:** `pwn.college{MfiMH-LyEzBfHstqtU7FTLa5JbV.QX3QDO0wSN0EzNzEzW}`

WSL terminal session:

```bash
hacker@processes~backgrounding-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running *and
not suspended* in this terminal... Let's check!

UID          PID STAT CMD
root         153 S+   bash /challenge/run
root         155 R+   ps -o user=UID,pid,stat,cmd

I don't see a second me!

To pass this level, you need to suspend me, resume the suspended process in the
background, and then launch a new version of me! You can background me with
Ctrl-Z (and resume me in the background with 'bg') or, if you're not ready to
do that for whatever reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~backgrounding-processes:~$ bg
[1]+ /challenge/run &
hacker@processes~backgrounding-processes:~$


Yay, I'm now running the background! Because of that, this text will probably
overlap weirdly with the shell prompt. Don't panic; just hit Enter a few times
to scroll this text out.
/challenge/run
I'll only give you the flag if there's already another copy of me running *and
not suspended* in this terminal... Let's check!

UID          PID STAT CMD
root         153 S    bash /challenge/run
root         163 S    sleep 6h
root         164 S+   bash /challenge/run
root         166 R+   ps -o user=UID,pid,stat,cmd

Yay, I found another version of me running in the background!
 Here is the flag:
pwn.college{MfiMH-LyEzBfHstqtU7FTLa5JbV.QX3QDO0wSN0EzNzEzW}
```

### My solve

Suspended the first instance with Ctrl-Z then used `bg` to resume it in the background. Launched a new instance to satisfy the requirement and received the flag.

### What I learned

`bg` resumes a stopped job in the background. Some checks require one instance running in background and another running in foreground.

---

## foregrounding-processes

**Flag:** `pwn.college{k8eBlWpQxiHpPzLYInJzVvYTTVo.QX4QDO0wSN0EzNzEzW}`

WSL terminal session:

```bash
hacker@processes~foregrounding-processes:~$ /challenge/run
To pass this level, you need to suspend me, resume the suspended process in the
background, and *then* foreground it without re-suspending it! You can
background me with Ctrl-Z (and resume me in the background with 'bg') or, if
you're not ready to do that for whatever reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~foregrounding-processes:~$ bg
[1]+ /challenge/run &
hacker@processes~foregrounding-processes:~$


Yay, I'm now running the background! Because of that, this text will probably
overlap weirdly with the shell prompt. Don't panic; just hit Enter a few times
to scroll this text out. After that, resume me into the foreground with 'fg';
I'll wait.

hacker@processes~foregrounding-processes:~$ fg
/challenge/run
YES! Great job! I'm now running in the foreground. Hit Enter for your flag!

pwn.college{k8eBlWpQxiHpPzLYInJzVvYTTVo.QX4QDO0wSN0EzNzEzW}
```

### My solve

Suspended the program, resumed it in the background with `bg`, and then used `fg` to bring it back to the foreground without re-suspending. The program then printed the flag.

### What I learned

You can cycle a job between background and foreground using `bg` and `fg` without re-suspending it. Order of operations matters for some interactive checks.

---

## starting-backgrounded-processes

**Flag:** `pwn.college{cLhgMsv5DjZeaLgFGeRTQ_i24U3.QX5QDO0wSN0EzNzEzW}`

WSL terminal session:

```bash
hacker@processes~starting-backgrounded-processes:~$ /challenge/run &
[1] 153
hacker@processes~starting-backgrounded-processes:~$


Yay, you started me in the background! Because of that, this text will probably
overlap weirdly with the shell prompt, but you're used to that by now...

Anyways! Here is your flag!
pwn.college{cLhgMsv5DjZeaLgFGeRTQ_i24U3.QX5QDO0wSN0EzNzEzW}
```

### My solve

Started the challenge with `&` to run it directly in the background. The program detected this and printed the flag.

### What I learned

Appending `&` launches a process in the background immediately. Background processes can be used to meet challenge conditions requiring concurrent running instances.

---

## process-exit-codes

**Flag:** `pwn.college{AKdyI0xOBKQdCAScbVz6el4sQKu.QX5YDO1wSN0EzNzEzW}`

WSL terminal session:

```bash
hacker@processes~process-exit-codes:~$ /challenge/get-code
/challenge/submit-code $?
Exiting with an error code!
CORRECT! Here is your flag:
pwn.college{AKdyI0xOBKQdCAScbVz6el4sQKu.QX5YDO1wSN0EzNzEzW}
```

### My solve

Ran `/challenge/get-code` which executed a command and then checked the exit code `$?`. The program reported an error code path and printed the flag when the expected code matched.

### What I learned

Commands return exit codes accessible via `$?`. Programs may check those codes to gate progress.

---
