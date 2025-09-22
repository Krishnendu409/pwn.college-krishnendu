# Intro to Arguments
*Module:* Hello Hackers (pwn.college)
**Date:** 2025-09-22

## My solve
**Flag:** `pwn.college{813EE-00GNaHrkob9ZqbdM29JVE.QX4YjM1wSN0EzNzEzW}`

## Steps
1. Connected via SSH: `ssh -i ~/key hacker@dojo.pwn.college`.
2. Typed the command with the argument: `hello hackers`.
3. Copied the flag from the output.

## Explanation
Commands can take arguments that modify their behavior. Here, the `hello` program required a single argument `hackers`. The shell splits input into command and arguments. The program read this argument and returned the flag. This demonstrates how arguments work and how they are passed to programs.

## What I learned
- How shell splits input into command + arguments.
- Arguments can change the output of a program.
- Linux commands and arguments are case-sensitive.

## References
Did not use any references for this challenge.
