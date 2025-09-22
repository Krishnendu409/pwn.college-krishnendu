# Intro to Command
*Module:* Hello Hackers (pwn.college)
**Date:** 2025-09-22

## My solve
**Flag:** `pwn.college{gpK8CJP2puAmJUMzUfDdjCc6voZ.QX3YjM1wSN0EzNzEzW}`

## Steps
1. Started the Hello Hackers session on pwn.college.
2. Connected via SSH using my key: `ssh -i ~/key hacker@dojo.pwn.college`.
3. At the prompt, typed the command: `hello`.
4. Copied the flag from the output.

## Explanation
This level teaches how to invoke a command in the shell. The shell parses the first token as the command and runs it. `hello` is a simple program that prints the flag. No arguments or extra steps are required. The focus is on getting comfortable with running commands in a remote session.

## What I learned
- How to start a dojo session and connect via SSH.
- How commands are parsed and executed by the shell.
- Flags can be obtained directly from simple challenge programs.

## References
Did not use any references for this challenge.
