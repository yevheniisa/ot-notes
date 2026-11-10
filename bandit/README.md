# OverTheWire Bandit

Linux in the terminal, one level at a time. Commands and what I learned, in my own words.
No passwords here: OverTheWire asks players not to publish them.

| Level | Command(s) | What I learned |
|---|---|---|
| 0 → 1 | `ssh bandit0@bandit.labs.overthewire.org -p 2220`, `ls`, `cat readme` | `ssh -p` connects on a non-default port. `ls` shows what's in a directory, `cat` prints a file. |
| 1 → 2 | `pwd`, `cat /home/bandit1/-` (shorter: `cat ./-`) | A bare `-` means stdin to `cat`, so it just waits for input. Giving a path to the file (`./-` or the full path) makes it read the file. |
| 2 → 3 | `cat -- "--spaces in this filename--"` | Spaces in a name: wrap it in quotes, or the shell splits it into several arguments. The name starts with `--`, so `--` in front tells cat "no more options, everything after is a file". |
| 3 → 4 | `cd inhere`, `ls -A`, `cat ...Hiding-From-You` | Files whose name starts with `.` are hidden from plain `ls`. `ls -A` shows them (`-a` also shows `.` and `..`). Hidden is just a naming convention, not protection. |
| 4 → 5 | `file -- -file07` (all at once: `file ./*`), then `cat ./-file07` | `file` tells the real type of a file by its content, not by its name. `-b` gives a short answer without the filename. `--` because the name starts with `-`. |

## Side notes
- `ls -la` permissions, e.g. `-rw-r-----  bandit3 bandit2`: owner can read/write, group can read, everyone else gets nothing. If you're not the owner or in the group, you get `Permission denied`.

