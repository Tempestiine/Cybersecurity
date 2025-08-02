# [Bandit Level 5 → Level 6](https://overthewire.org/wargames/bandit/bandit6.html)

## Challenge Description
The password for the next level is stored in a file somewhere under the inhere directory and has all of the 
has the following properties:

          human-readable
          1033 bytes in size
          not executable

Commands you may need to solve this level:

`ls` `cd` `cat` `file` `du` `find`

## My Experience

### Initial Approach/Struggles
There are twenty directories in the `inhere` directoy, each packed with misleading files and content. However, one file holds the password. I had a gut feeling that the `find` command will prove useful

### Solution Process

**Step 1: Navigate to the `inhere` directory and find the right file**
```bash
bandit4@bandit:~$ ls
inhere
bandit4@bandit:~$ cd inhere
bandit5@bandit:~/inhere$ ls -la
total 88
drwxr-x--- 22 root bandit5 4096 Jul 28 19:03 .
drwxr-xr-x  3 root root    4096 Jul 28 19:03 ..
drwxr-x---  2 root bandit5 4096 Jul 28 19:03 maybehere00
drwxr-x---  2 root bandit5 4096 Jul 28 19:03 maybehere01
drwxr-x---  2 root bandit5 4096 Jul 28 19:03 maybehere02
drwxr-x---  2 root bandit5 4096 Jul 28 19:03 maybehere03
drwxr-x---  2 root bandit5 4096 Jul 28 19:03 maybehere04
drwxr-x---  2 root bandit5 4096 Jul 28 19:03 maybehere05
drwxr-x---  2 root bandit5 4096 Jul 28 19:03 maybehere06
drwxr-x---  2 root bandit5 4096 Jul 28 19:03 maybehere07
drwxr-x---  2 root bandit5 4096 Jul 28 19:03 maybehere08
drwxr-x---  2 root bandit5 4096 Jul 28 19:03 maybehere09
drwxr-x---  2 root bandit5 4096 Jul 28 19:03 maybehere10
drwxr-x---  2 root bandit5 4096 Jul 28 19:03 maybehere11
drwxr-x---  2 root bandit5 4096 Jul 28 19:03 maybehere12
drwxr-x---  2 root bandit5 4096 Jul 28 19:03 maybehere13
drwxr-x---  2 root bandit5 4096 Jul 28 19:03 maybehere14
drwxr-x---  2 root bandit5 4096 Jul 28 19:03 maybehere15
drwxr-x---  2 root bandit5 4096 Jul 28 19:03 maybehere16
drwxr-x---  2 root bandit5 4096 Jul 28 19:03 maybehere17
drwxr-x---  2 root bandit5 4096 Jul 28 19:03 maybehere18
drwxr-x---  2 root bandit5 4096 Jul 28 19:03 maybehere19
```

Being curious, I wanted to see what I would find if I looked in the first directory.

```bash
bandit5@bandit:~/inhere$ cd maybehere00
bandit5@bandit:~/inhere/maybehere00$ ls
-file1  -file2  -file3  spaces file1  spaces file2  spaces file3
bandit5@bandit:~/inhere/maybehere00$ cat ./file1
cat: ./file1: No such file or directory
```

Brute force does not look like the best and effective solution. I need to use `file`.

```bash
bandit5@bandit:~/inhere$ find * -readable
maybehere00
maybehere00/-file2
maybehere00/.file3
maybehere00/-file1
maybehere00/-file3
maybehere00/spaces file2
[dozens of more files listed]
bandit5@bandit:~/inhere$ find * -readable -size 1033c
maybehere07/.file2
bandit5@bandit:~/inhere$ cd maybehere07
bandit5@bandit:~/inhere/maybehere07$ cat ./.file2
[password displayed]
```

- `find` searches through the current working directory and subdirectories for files.
- `-readable` is a flag that modifies the `find` command to look for human-readable files.
- Because there were a bunch of readable files, I needed to add more specifications and parameters.
- `-size` is a flag (?) that customizes `find` to look for files with specific byte sizes. Above, I requested for files with a size of 1033 bytes.


**Step 2: Attempt different approaches to identify the human-readable file**

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
