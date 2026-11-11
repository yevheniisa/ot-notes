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
| 5 → 6 | `find . -type f -size 1033c ! -executable` | `find` searches from a starting dir (`.` = here). `-type f` files only, `-size 1033c` exactly 1033 bytes (`c` = bytes), `!` negates the next test, so `! -executable` = not executable. |
| 6 → 7 | `find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null` | Search the whole server from `/`. `-size 33b` would be 33 blocks of 512 bytes, `33c` is 33 bytes. Output has two streams: 1 = stdout (results), 2 = stderr (errors). `> /dev/null` throws away the results; `2>/dev/null` throws away only the errors. |
| 7 → 8 | `grep -w millionth data.txt` | `grep` prints only the lines that contain a pattern. `-w` matches the whole word, so `millionth` won't also hit `millionths`. Same tool for searching logs. |
| 8 → 9 | `sort data.txt \| uniq -u` | `uniq` only compares a line with the one right before it, so duplicates far apart slip through. `sort` puts identical lines next to each other first. `-u` prints only lines that appear once. `\|` (pipe) feeds one command's output into the next. |
| 9 → 10 | `strings data.txt \| grep '=='` | `strings` pulls the human-readable text out of a binary file (sequences of 4+ printable characters). Then `grep` keeps the lines with several `=`. `-w` isn't needed here; `==` already says "several". |
| 10 → 11 | `base64 -d data.txt` (or `cat data.txt \| base64 -d`) | `base64 -d` decodes. Base64 is encoding, not encryption: anyone can reverse it, no key needed. HTTP Basic auth sends credentials this way, so on an unencrypted network they're readable by anyone sniffing. |
| 11 → 12 | `tr 'A-Za-z' 'N-ZA-Mn-za-m' < data.txt` | ROT13: each letter moves 13 places, so A-M ↔ N-Z (same for lowercase); doing it twice gives the original. `tr` only reads stdin and takes two sets, no filename: feed the file with `<` or `cat file \|`. ROT13 is hiding, not security. |

## Side notes
- `ls -la` permissions, e.g. `-rw-r-----  bandit3 bandit2`: owner can read/write, group can read, everyone else gets nothing. If you're not the owner or in the group, you get `Permission denied`.