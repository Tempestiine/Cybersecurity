# [Bandit Level 5 → Level 6](https://overthewire.org/wargames/bandit/bandit6.html)

## Challenge Description
The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:

          human-readable
          1033 bytes in size
          not executable

Commands you may need to solve this level:

`ls` `cd` `cat` `file` `du` `find`

## My Experience

### Initial Approach/Struggles
Trying to filter my search for human-readable files proved difficult. I knew what I wanted to accomplish, but it was hard to find the right command to execute my idea. I could use brute force to check each file individually, but realistically I wouldn't learn much if I cheated.

### Solution Process

**Step 1: Navigate to the `inhere` directory and explore the files**
```bash
bandit4@bandit:~$ ls
inhere
bandit4@bandit:~$ cd inhere
bandit4@bandit:~/inhere$ ls
-file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09
```

**Step 2: Attempt different approaches to identify the human-readable file**
```bash
bandit4@bandit:~/inhere$ ls -h
-file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09
bandit4@bandit:~/inhere$ cat ./-file00
,9KL��+ӑ�'��,�BtZ�@P0N��Q��
bandit4@bandit:~/inhere$ ls -lsh
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
```
- The `-h` flag didn't reveal which file was human-readable
- When I tested the first file with `cat`, it displayed random characters and symbols
- Using `ls -lsh` showed that all files have the same size and permissions, so there were no obvious differences

**Step 3: Use the `file` command to identify file types**
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
[password displayed]
```
- The `file` command identified `-file07` as an `ASCII text` file while all others were labeled as `data`
- `file` is a command that determines the file type of each file
- The asterisk (`*`) is a wildcard character that allows me to select all files in the directory at once
- I quickly read the ASCII text file with `cat` and obtained the password

## What I Learned

### New Commands/Concepts
1. **File type identification**: The `file` command can distinguish between different file formats, even when they appear similar
2. **Wildcard usage**: The `*` character allows operations on multiple files simultaneously
3. **Efficient searching**: Instead of checking files individually, using tools like `file` can quickly analyze multiple files

## Real-World Applications
- **Digital forensics**: Investigators need to quickly identify file types when examining seized devices, as malicious files are often disguised or have misleading extensions. I can imagine using it to avoid possible red herrings
- **System administration**: When troubleshooting systems, administrators need to distinguish between configuration files (text) and data files
- **Malware analysis**: Security professionals use file type identification to determine how to properly analyze suspicious files
- **Data recovery**: When recovering corrupted files, identifying the actual file type helps determine the appropriate recovery method

## Key Takeaway
Understanding file types and having the right tools to identify them is vital in cybersecurity work. The `file` command is an essential tool for quickly analyzing unknown files, a skill I could use in security analysis and system administration. Learning to work efficiently with multiple files using wildcards also saves significant time when dealing with large datasets.
