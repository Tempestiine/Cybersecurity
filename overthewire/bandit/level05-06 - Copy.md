# [Bandit Level 5 → Level 6](https://overthewire.org/wargames/bandit/bandit6.html)

## Challenge Description
The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:

- human-readable
- 1033 bytes in size
- not executable

Commands you may need to solve this level:
`ls` `cd` `cat` `file` `du` `find`

## My Experience

### Initial Approach/Struggles
There are twenty directories in the `inhere` directory, each packed with misleading files and content. However, one file holds the password. I had a gut feeling that the `find` command would prove useful for this challenge, especially with all the specific criteria given.

### Solution Process

**Step 1: Navigate to the `inhere` directory and assess the scope**
```bash
bandit5@bandit:~$ ls
inhere
bandit5@bandit:~$ cd inhere
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

**Step 2: Explore one directory to understand the challenge scope**
```bash
bandit5@bandit:~/inhere$ cd maybehere00
bandit5@bandit:~/inhere/maybehere00$ ls
-file1  -file2  -file3  spaces file1  spaces file2  spaces file3
bandit5@bandit:~/inhere/maybehere00$ cat ./-file1
cat: ./-file1: No such file or directory
```

Being curious, I wanted to see what I would find in the first directory. After seeing multiple files in just one directory, it became clear that brute force checking each file individually would not be the most effective solution.

**Step 3: Use `find` with specific criteria**
```bash
bandit5@bandit:~/inhere$ cd ..
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
bandit5@bandit:~/inhere$ cat ./maybehere07/.file2
[password displayed]
```

- `find` searches through the current working directory and all subdirectories for files
- `-readable` is a flag that modifies the `find` command to look for human-readable files only
- Because there were dozens of readable files, I needed to add more specific parameters to narrow down the search
- `-size 1033c` is an option that customizes `find` to look for files with exactly 1033 bytes in size. The `c` stands for bytes (characters)
- After solving the challenge independently, I compared my process with other hackers, who included the command `grep` and used pipes `|` to find the solution. I wasn't recommended those commands by Bandit for this level, but they seem just as useful.

## What I Learned

### New Commands/Concepts
1. **Advanced `find` command usage**: The `find` command can combine multiple criteria to efficiently locate specific files
2. **File size specification**: The `-size` option with `c` suffix allows searching by exact byte count
3. **Systematic searching**: Instead of manual checking, using multiple filters can quickly narrow down results from hundreds of files to just one
4. **Command combination**: Multiple flags can work together to create precise search queries

## Real-World Applications
- **Digital forensics**: Investigators need to locate specific files among thousands based on criteria like size, type, and permissions when analyzing seized devices
- **System administration**: When troubleshooting systems, administrators often need to find configuration files or logs that match specific characteristics
- **Security auditing**: Security professionals search for files with unusual permissions, sizes, or types that might indicate compromise or misconfiguration
- **Data management**: In large file systems, efficiently locating files with specific properties is essential for maintenance and organization
- **Incident response**: During security incidents, quickly finding files that match attack indicators helps speed up investigation and containment

## Key Takeaway
Instead of manually checking hundreds of files, I learned to use the `find` command's filtering capabilities to narrow down results systematically. Often in cyber work, you need to locate specific files among massive datasets during investigations, audits, or incident response. Constructing precise search queries saves significant time and ensures thorough coverage.
