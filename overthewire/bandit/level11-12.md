# [Bandit Level 11 → Level 12](https://overthewire.org/wargames/bandit/bandit12.html)

## Challenge Description
The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions.

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

**Helpful Reading Material**

[Rot13 on Wikipedia](https://en.wikipedia.org/wiki/ROT13)

## My Experience

### Initial Approach/Struggles
I was struggling with using the `tr` command properly, so I referred to the reading material given by Bandit. Having read the Wikipedia, all I needed to do was read the file and translate the characters within it using ROT13.

### Solution Process

**Translate the file** ✓

```bash
bandit11@bandit:~$ cat data.txt
Gur cnffjbeq vf 7k16JArUVv5LxVuJfsSVdbbtaHGlw9D4
bandit11@bandit:~$ strings data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
The password is [password displayed]
```

- `tr` is a tool to translate, insert, or delete characters. This is important for cryptography
- After translating the text in `data.txt` by 13 characters using ROT13, I got the password in plain English

```bash
bandit11@bandit:~$ strings data.txt | tr 'a-zA-Z' 'n-za-mN-ZA-M'
```

- This alternative command also works and gives the same solution

## What I Learned

### New Commands/Concepts
1. **ROT13 Cipher**: A simple cipher that shifts each letter 13 positions in the alphabet
2. **`tr` Command**: Translates, squeezes, or deletes characters from input
3. **Character Ranges**: Understanding how to specify ranges like 'A-Z' and 'a-z' for both uppercase and lowercase letters

## Real-World Applications
**Malware Obfuscation**: Attackers use simple ciphers like ROT13 to hide malicious code from basic detection systems that only scan for readable strings.

**Data Exfiltration**: Security analysts might find encoded data in logs or files that attackers used to hide stolen information

> **Specific Example**: A security analyst finds suspicious text in a log file that looks scrambled. They suspect ROT13 encoding and decode it:

```bash
# Decode suspicious ROT13 text
echo "frperg_onpxqbbe_freire" | tr 'a-zA-Z' 'n-za-mN-ZA-M'
# Output: secret_backdoor_server
```

## Key Takeaway
Basic ciphers are still used today because they're quick to implement and can trick automated scanning tools. Understanding character translation with `tr` is fundamental for cybersecurity professionals who need to decode data during investigations.
