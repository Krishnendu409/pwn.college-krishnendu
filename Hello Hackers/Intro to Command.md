# Command History
*Module:* Hello Hackers (pwn.college)
**Date:** 2025-09-22

## My solve
**Flag:** `pwn.college{gpK8CJP2puAmJUMzUfDdjCc6voZ.QX3YjM1wSN0EzNzEzW}`

## Steps
1. Logged in via SSH.
2. Pressed the up arrow key in the terminal to scroll through previous commands.
3. Found the flag in the history and copied it.

## Explanation
This challenge taught how the shell saves command history. Instead of retyping, we can scroll through past commands. The flag was stored as one of the previous commands, so using the arrow keys made it easy to retrieve.

## What I learned
- How to use command history in Linux.
- That you can reuse previous commands instead of typing everything again.
- Flags can sometimes be hidden in history.

## References
Did not use any references for this challenge.
