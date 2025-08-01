# [Bandit Level 2 → Level 3](https://overthewire.org/wargames/bandit/bandit3.html)

## Challenge Description
The password for the next level is stored in a file called –spaces in this filename– located in the home directory.

Commands you may need to solve this level:
`ls` `cd` `cat` `file` `du` `find`

[Google Search for "spaces in filename"](https://www.google.com/search?q=spaces+in+filename)

## My Experience

### Initial Approach/Struggles
I couldn't read the file because there were spaces. The `cat` command percieved the filename as arguments and parameters when reading `--spaces in this filename--`.

### Solution Process

**Step 1: Attempt to read the file**

```bash
bandit2@bandit:~$ ls -l
total 4
-rw-r----- 1 bandit3 bandit2 33 Jul 28 19:03 --spaces in this filename--
bandit2@bandit:~$ cat --spaces in this filename--
cat: unrecognized option '--spaces'
Try 'cat --help' for more information.
```

- It seems like the file is specially named, just like the last level's file which contained the password.
- I wanted to test the other commands provided by Bandit and see if they would shed any light after trying out `cat` one more time.

**Step 2: Try again**
```bash
bandit2@bandit:~$ cat ./--spaces in this filename--
cat: ./--spaces: No such file or directory
cat: in: No such file or directory
cat: this: No such file or directory
cat: filename--: No such file or directory
```
```bash
bandit2@bandit:~$ find *
find: unknown predicate `--spaces in this filename--'
```

- `find` searches for any 

## What I Learned

### New Commands/Concepts
1. I have to modify the `cat` command when trying to read files with special characters
2. Some commands implicitly add `./` at the beginning, but when dealing with special characters, I need to be explicit
3. The `-` character has special meaning in Linux (represents stdin/stdout), so it can't be used directly as a filename in commands

## Real-World Applications
- **Security assessment**: Attackers might try to hide malicious files using special characters, thinking they're harder to access
- **System administration**: Understanding how to handle files with unusual names is crucial when cleaning up systems or investigating suspicious activity
- **File forensics**: You might encounter files with special characters that require specific techniques to examine

## Key Takeaway
Naming a file with special characters does not protect against hackers accessing private content. In fact, understanding how to handle these cases is an essential skill for cybersecurity professionals. This level taught me that the command line has specific rules for handling special characters, and learning these rules makes me more capable of navigating any system I encounter.
