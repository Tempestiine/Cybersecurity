# [Bandit Level 9 → Level 10](https://overthewire.org/wargames/bandit/bandit10.html)

## Challenge Description
The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several '=' characters.

Commands you may need to solve this level:

| Command | What It Does |
|---------|--------------|
| `strings` | Extracts human-readable text from binary files |
| `grep` | Searches for patterns in text |
| `man` | Shows manual pages for commands |
| `sort` | Arranges lines, text, and data |
| `uniq` | Filters out duplicate adjacent lines |
| `base64` | Encodes and decodes base64 data |

## My Experience

### Initial Approach/Struggles
This challenge was easier than I thought. Given that data files likely contain binary data mixed with readable strings, I need to filter for lines containing the '=' pattern.

### Solution Process
**Find the password with `grep`** ✓
```bash
bandit9@bandit:~$ strings data.txt | grep "="
Pw=h
========== the
C%m=
y7{1Z=
========== passwordb
#[q?=p
F========== is;o|
@[W=
p?e=    v
 K=r
V9V=]
U========== [password displayed]
u5=R
```
- The `strings` command extracted all human-readable text from the binary file
- `grep "="` filtered for lines containing the equals sign, as specified in the challenge
- Above, the results read, "the password is [password]."

## What I Learned

### New Commands/Concepts
1. **Pattern Recognition**: Learning to visually scan command output for meaningful patterns (in this case, the sentence structure "the password is...")

## Real-World Applications

**Digital Forensics**: Investigators extract readable content from memory dumps or corrupted files to find evidence like passwords, usernames, or file paths.

> **Specific Example**: A forensics analyst examining a suspected malware sample needs to find any embedded URLs or domain names:
```bash
# Extract readable strings from malware binary, then search for web-related patterns
strings suspicious_file.exe | grep -E "(http|www|\.com|\.net)"
```

## Key Takeaway
Combining `strings` with pattern matching tools like `grep` can make a powerful tool for finding a needle in a giant, digital haystack. In the real world, everything is not neatly put in text files with ASCII values.
