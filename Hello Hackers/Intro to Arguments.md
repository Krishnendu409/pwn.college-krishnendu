# Intro to Arguments
*Module:* Hello Hackers (pwn.college)
**Date:** 2025-09-22

## My solve
**Flag:** `pwn.college{813EE-00GNaHrkob9ZqbdM29JVE.QX4YjM1wSN0EzNzEzW}`

## Steps
1. Logged in via SSH.
2. Typed `hello hackers` at the prompt.
3. Copied the flag from the output.

## Explanation
This challenge showed how commands can take arguments. Here, `hackers` was an argument to `hello`. The shell splits what you type into the command and arguments, and the program returned the flag based on that.

## What I learned
- How to pass arguments to commands.
- How Linux parses command + arguments.
- That small differences (like case) can matter.

## References
Did not use any references for this challenge.
