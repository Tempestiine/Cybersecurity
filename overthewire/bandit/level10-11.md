# [Bandit Level 10 → Level 11](https://overthewire.org/wargames/bandit/bandit11.html)

## Challenge Description
The password for the next level is stored in the file data.txt, which contains base64 encoded data.

Commands you may need to solve this level:
`man` `grep` `sort` `uniq` `strings` `base64` `tr` `tar` `gzip` `bzip2` `xxd`

## Command Reference Table
| Command | What It Does |
|---------|--------------|
| `base64` | Encodes and decodes base64 data |
| `strings` | Extracts human-readable text from binary files |
| `grep` | Searches for patterns in text |
| `man` | Shows manual pages for commands |
| `sort` | Arranges lines, text, and data |
| `uniq` | Filters out duplicate adjacent lines |

## My Experience

### Initial Approach/Struggles
I used `base64` to decode the file, and I got the password to the next level. This was pretty straightforward.

### Solution Process
**Decode the file** ✓

```bash
bandit10@bandit:~$ strings data.txt
VGhlIHBhc3N3b3JkIGlzIGR0UjE3M2ZaS2IwUlJzREZTR3NnMlJXbnBOVmozcVJyCg==
bandit10@bandit:~$ base64 -d data.txt
The password is dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```

- `base64` is used to encode binary data as printable text. It's like hexcode or morse code!
- Some common characteristics of base64 include uppercase letters (A-Z), lowercase letters (a-z), digits (0-9), and the equals sign (=) for padding at the end
- I decoded `data.txt` with the `-d` flag, and I found the answer in plain English

## What I Learned

### New Commands/Concepts
1. **Base64 Encoding/Decoding**: A method to convert binary data into ASCII text using 64 printable characters
2. **Pattern Recognition**: Learning to identify base64 by its characteristic format
3. **Data Obfuscation**: Understanding that readable data can be disguised in encoded formats
4. **Command Flags**: Using `base64 -d` to decode (decrypt) versus `base64` alone to encode

## Real-World Applications
**Malware Analysis**: Attackers often hide malicious payloads in base64 to bypass basic security filters that only scan for readable text.

**Web Security**: Security analysts decode base64-encoded data in HTTP requests to find hidden attack payloads or sensitive information leakage.

> **Specific Example**: A security analyst investigating a suspicious web request finds base64 data in a POST parameter. They need to decode it to see if it contains malicious code:
```bash
echo "PD9waHAgZXZhbCgkX1BPU1RbJ2NtZCddKTs/Pg==" | base64 -d
# Output: <?php eval($_POST['cmd']);?>  (malicious PHP code!)
```

This same technique helps with:
- **Email Security**: Decoding base64 attachments that might contain malware
- **Network Forensics**: Analyzing encoded data in network traffic captures
- **Incident Response**: Revealing hidden commands or data in system logs

## Key Takeaway
Files that seem like random jargon or can't be read may be misleading. Attackers can use encoding to hide malicious content. Never overlook files that appear to be gibberish without first checking if they might be encoded data.
