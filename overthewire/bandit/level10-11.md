# [Bandit Level 9 → Level 10](https://overthewire.org/wargames/bandit/bandit10.html)

## Challenge Description
The password for the next level is stored in the file data.txt, which contains base64 encoded data

Commands you may need to solve this level:

| Command | What It Does |
|---------|--------------|
| `strings` | Extracts human-readable text from binary files |
| `grep` | Searches for patterns in text |
| `man` | Shows manual pages for commands |
| `sort` | Arranges lines, text, and data |
| `uniq` | Filters out duplicate adjacent lines |
| `base64` | Encodes and decodes base64 data |

---

## My Experience

### Initial Approach/Struggles
I used `base64` to decode the file, and I got the password to the next level

### Solution Process
**Decode the file** ✓
```bash
bandit10@bandit:~$ strings data.txt
VGhlIHBhc3N3b3JkIGlzIGR0UjE3M2ZaS2IwUlJzREZTR3NnMlJXbnBOVmozcVJyCg==
bandit10@bandit:~$ base64 -d data.txt
The password is dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```

- `base64` is used to encode binary data as printable text. It's like hexcode or morse code!
- Some common characteristics of base64  may include...Uppercase letters (A-Z) Lowercase letters (a-z Digits (0-9) Equals sign (=) for padding at the end.

- I decoded `data.txt`, and I found the answer.

---

## What I Learned

### New Commands/Concepts
Decoding.
Base64
how to identify it


(OLD)
1. **Pattern Recognition**: Learning to visually scan command output for meaningful patterns (in this case, the sentence structure "the password is...")

## Real-World Applications
wouldn't people try to hide sensitive information in base64?
or what if you wanted to send over or collect information, and base64 is the only way because regular information or text is too BIG? or small?
or what if you're trying to send secret messages like in i think its called cryptography? you're workihg for tye cia.
you encode and decode to save memory and space?

(OLD)
**Digital Forensics**: Investigators extract readable content from memory dumps or corrupted files to find evidence like passwords, usernames, or file paths.

> **Specific Example**: A forensics analyst examining a suspected malware sample needs to find any embedded URLs or domain names. They extract readable strings from the file and search for web-related patterns.

```bash
strings suspicious_file.exe | grep -E "(http|www|\.com|\.net)"
```

## Key Takeaway
files that seem like jargon or can't be read may be misleading. i can not overlook files? decoding is an essential skill?

(old)
Combining `strings` with pattern matching tools like `grep` can make a powerful tool for finding a needle in a giant, digital haystack. In the real world, everything is not neatly put in text files with ASCII values.
