# [Bandit Level 11 → Level 12](https://overthewire.org/wargames/bandit/bandit12.html)

## Challenge Description
The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

Commands you may need to solve this level:

## Command Reference Table
| Command | What It Does |
|---------|--------------|
| `grep` | Searches for patterns in text |
| `sort` | Arranges lines, text, and data |
| `uniq` | Filters out duplicate adjacent lines |
| `strings` | Extracts human-readable text from binary files |
| `base64` | Encodes and decodes base64 data |
| `tr` | Translates or deletes characters |
| `tar` | Archives and extracts files |
| `gzip` | Compresses and decompresses files |
| `bzip2` | Compresses and decompresses files (better compression) |
| `xxd` | Creates hex dumps or reverses them |

Helpful Reading Material

[Rot13 on Wikipedia](https://en.wikipedia.org/wiki/ROT13)

## My Experience

### Initial Approach/Struggles
I was struggling with using the `tr` command properly, so I referred to the reading material given by Bandit. Having read wikipedia, all I needed to do is to read the file and translate the characters within it.

### Solution Process
**Translate the file** ✓

```bash
bandit11@bandit:~$ cat data.txt
Gur cnffjbeq vf 7k16JArUVv5LxVuJfsSVdbbtaHGlw9D4
bandit11@bandit:~$ strings data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
The password is [password displayed]
```

- `tr` is a tool to translate characters, insert, or delete characters. This is important for cryptography.
- After translating the text in `data.txt` by 13 characters, I got the password.

```bash
bandit11@bandit:~$ strings data.txt | tr 'a-zA-Z' 'n-za-mN-ZA-M'
```

- This command also works too and gives the same solution

## What I Learned

### New Commands/Concepts?

cryptography? people may try to send hidden messages to others within files.
`tr`
- how to translate characters.

## Real-World Applications
You can intercept code. Imagine if you were in the CIA or FBI. very cool.
This was used during the Cold War, I bet.
insert some malicious code into files on purpose to gain access to someone's computer or run some hidden commands with 'tr', maybe with that php code.
insert and delete code to ruin the message or text in the hidden file with `tr`

[insert specific example]


## Key Takeaway
You can translate to read content that's encrypted with `tr`. This is important for cybersecurity if you're working with the GRC.
