# Command History
*Module:* Hello Hackers (pwn.college)
**Date:** 2025-09-22

## My solve
**Flag:** `pwn.college{sQPNpNBFIzIxw1pWnqI3qUYjYp4.0lNzEzNxwSN0EzNzEzW}`

## Steps
1. Opened the SSH session: `ssh -i ~/key hacker@dojo.pwn.college`.
2. Used the up-arrow key to access previous commands stored in shell history.
3. Retrieved the injected flag from the history output.

## Explanation
The shell saves a history of all commands typed. Using the arrow keys, you can scroll through previous commands instead of typing them again. This challenge demonstrates how flags or important info may appear in shell history, reinforcing the usefulness of command recall.

## What I learned
- How to use command history efficiently.
- Commands can be repeated without retyping.
- Some challenges store flags in history for practice.

## References
Did not use any references for this challenge.
