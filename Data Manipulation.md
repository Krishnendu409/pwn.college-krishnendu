# deleting-characters

## My solve

**Flag:** `pwn.college{gHmRwCXEYBgJUvju_U0JXPkq-GO.0FNxEzNxwSN0EzNzEzW}`

Used `tr -d '^%'` to remove the decoy characters `^` and `%` from the program output.

```bash
/challenge/run | tr -d '^%'
# Output:
pwn.college{gHmRwCXEYBgJUvju_U0JXPkq-GO.0FNxEzNxwSN0EzNzEzW}
```

## What I learned

`tr -d` deletes specified characters from a stream. Useful for cleaning character-stuffed flags.

## References

`man tr`

# deleting-newlines

## My solve

**Flag:** `pwn.college{ofMtTDwT253QwFci-3ziD29D7Ka.0VNxEzNxwSN0EzNzEzW}`

Used `tr -d '\n'` to remove newline characters so the flag appears on a single line.

```bash
/challenge/run | tr -d '\n'
# Output:
pwn.college{ofMtTDwT253QwFci-3ziD29D7Ka.0VNxEzNxwSN0EzNzEzW}
```

## What I learned

`tr -d '\n'` collapses multi-line output into one line.

## References

`man tr`

# extracting-the-first-lines-with-head

## My solve

**Flag:** `pwn.college{YrMdxveGInlyW6lu-1j5bUF9kXr.0lNxEzNxwSN0EzNzEzW}`

Used `head -n 7` to capture the first seven lines and piped them into the next program.

```bash
/challenge/pwn | head -n 7 | /challenge/college
# Output:
pwn.college{YrMdxveGInlyW6lu-1j5bUF9kXr.0lNxEzNxwSN0EzNzEzW}
```

## What I learned

`head -n` extracts the first N lines; piping allows passing only the required lines downstream.

## References

`man head`

# extracting-specific-sections-of-text

## My solve

**Flag:** `pwn.college{IuAwxvrKpykqpZZb7Jpq-_Q59mN.01NxEzNxwSN0EzNzEzW}`

Used `cut -d " " -f 2` to select the second field and removed the newline with `tr -d '\n'`.

```bash
/challenge/run | cut -d " " -f 2 | tr -d '\n'
# Output:
pwn.college{IuAwxvrKpykqpZZb7Jpq-_Q59mN.01NxEzNxwSN0EzNzEzW}
```

## What I learned

`cut -d` isolates delimited fields; combine with `tr` to format single-line output.

## References

`man cut`
`man tr`

# sorting-data

## My solve

**Flag:** `pwn.college{sfTq62ewBBTUMI55tyaKwUJ_rrE.0FM0MDOxwSN0EzNzEzW}`

Sorted the flags file and used `tail -n 1` to pick the last (lexicographically largest) line.

```bash
sort /challenge/flags.txt | tail -n 1
# Output:
pwn.college{sfTq62ewBBTUMI55tyaKwUJ_rrE.0FM0MDOxwSN0EzNzEzW}
```

## What I learned

`sort` orders text lines; `tail -n 1` retrieves the final line. Combine to extract max/min entries.

## References

`man sort`
`man tail`

# translating-characters

## My solve

**Flag:** `pwn.college{wIMawUjmG1XfmEldKUrUdrjJy6i.01MxEzNxwSN0EzNzEzW}`

Used `tr 'A-Za-z' 'a-zA-Z'` to swap uppercase and lowercase characters.

```bash
/challenge/run | tr 'A-Za-z' 'a-zA-Z'
# Output:
pwn.college{wIMawUjmG1XfmEldKUrUdrjJy6i.01MxEzNxwSN0EzNzEzW}
```

## What I learned

`tr` can translate character ranges; mapping `A-Za-z` to `a-zA-Z` swaps cases.

## References

`man tr`
