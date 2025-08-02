# [Bandit Level 4 → Level 5](https://overthewire.org/wargames/bandit/bandit5.html)

## Challenge Description
The password for the next level is stored in the only human-readable file in the inhere directory.

Commands you may need to solve this level:
`ls` `cd` `cat` `file` `du` `find`

 Tip: if your terminal is messed up, try the “reset” command.

## My Experience

### Initial Approach/Struggles
Trying to filter my search for human-readable files proved difficult. I know what I want, but it was hard to find the right command to execute my idea. I could use brute force to find the password, but realistically I won't learn much if I cheat.

### Solution Process

**Step 1: Navigate to the `inhere` directory and identify the human-readable file**
```bash
bandit4@bandit:~$ ls
inhere
bandit4@bandit:~$ cd inhere
bandit4@bandit:~/inhere$ ls
-file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09
```

```bash
bandit4@bandit:~/inhere$ ls -h
-file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09
bandit4@bandit:~/inhere$ cat ./-file00
,9KL��+ӑ�'��,�BtZ�@P0N��Q��
bandit4@bandit:~/inhere$ ls -l -s -h
total 40K
4.0K -rw-r----- 1 bandit5 bandit4 33 Jul 28 19:03 -file00
4.0K -rw-r----- 1 bandit5 bandit4 33 Jul 28 19:03 -file01
4.0K -rw-r----- 1 bandit5 bandit4 33 Jul 28 19:03 -file02
4.0K -rw-r----- 1 bandit5 bandit4 33 Jul 28 19:03 -file03
4.0K -rw-r----- 1 bandit5 bandit4 33 Jul 28 19:03 -file04
4.0K -rw-r----- 1 bandit5 bandit4 33 Jul 28 19:03 -file05
4.0K -rw-r----- 1 bandit5 bandit4 33 Jul 28 19:03 -file06
4.0K -rw-r----- 1 bandit5 bandit4 33 Jul 28 19:03 -file07
4.0K -rw-r----- 1 bandit5 bandit4 33 Jul 28 19:03 -file08
4.0K -rw-r----- 1 bandit5 bandit4 33 Jul 28 19:03 -file09
bandit4@bandit:~/inhere$ find * -readable
find: unknown predicate `-file00'
```

- For some reason, the `-h` flag did not reveal the human-readable file
- Curious, I looked at the first file with `cat`, and it had a bunch of jargon
- I tried `ls -l`, but I didn't see any unique information among the files
- The `find` command didn't provide much either. `find` searches through files through the directory, and I wanted Terminal to identify readable ones.

```bash
bandit4@bandit:~/inhere$ file ./*
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data
bandit4@bandit:~/inhere$ cat ./-file07
[password]
```

- `file` spotlighted `-file07` as an `ASCII text` file. Quickly, I read it with `cat` and obtained the password.
- `file` is a command that determines the file type. The asterisk (`*`) after file is a wildcard, which is a special character that allows me to select groups of files.

## What I Learned

### New Commands/Concepts
1. **File appearances**: Data files and ASCII files are different, but they appear similar
2. **`file` command**: Great for identifying file types
   ?

## Real-World Applications
- **System configuration**: ? Guessing. Many config files hold various data for programs, and it's hard to discern them from regularing text files.
- **Security investigations**: Hidden files are commonly used to store malicious scripts or files that attackers don't want easily discovered
- **System administration**: Administrators need to check hidden files when troubleshooting user environments or investigating system issues
- **Software development**: Development tools often store configuration in hidden directories (like `.git`, `.vscode`) that need to be accessed for troubleshooting

## Key Takeaway
Understanding hidden files is fundamental. Both legitimate system files and potentially malicious files can be hidden. The ability to systematically search for and examine hidden files is a core skill that applies to system administration, security analysis, and digital forensics.
