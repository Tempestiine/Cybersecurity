# [Bandit Level 4 → Level 5](https://overthewire.org/wargames/bandit/bandit5.html)

## Challenge Description
The password for the next level is stored in a hidden file in the inhere directory.

Commands you may need to solve this level:
`ls` `cd` `cat` `file` `du` `find`

## My Experience

### Initial Approach/Struggles
This challenge was pretty straightforward compared to the previous levels. The main thing I needed to figure out was how to find hidden files in Linux.

### Solution Process

**Step 1: Navigate to the `inhere` directory**
```bash
bandit3@bandit:~$ ls -l
total 4
drwxr-xr-x 2 root root 4096 Jul 28 19:03 inhere
bandit3@bandit:~$ cd inhere
bandit3@bandit:~/inhere$ ls
bandit3@bandit:~/inhere$ ls -l
total 0
```
- `cd` transfers the user to a directory. In this case, I moved to the `inhere` directory
- Using `ls` and `ls -l` didn't work. As you can see above, the commands don't reveal any hidden files

**Step 2: Find and access the hidden file**
```bash
bandit3@bandit:~/inhere$ ls -a
.  ..  ...Hiding-From-You
bandit3@bandit:~/inhere$ cat "./...Hiding-From-You"
[password]
```
- I tried the flag `-a` because I wanted Terminal to show all possible files, including hidden ones
- The `-a` flag tells Terminal to not ignore entries starting with `.`
- On my screen in Kali Linux Terminal, I noticed that directories have a bold, blue font while files are in plain white text. I noticed that `.` is a directory representing the current directory, and `..` refers to the parent directory (the place before I did `cd inhere`). This visual distinction is handy for discerning what is a directory and what is a filename

**Step 3: Exploring flag combinations**
```bash
bandit3@bandit:~$ ls -la
total 24
drwxr-xr-x   3 root root 4096 Jul 28 19:03 .
drwxr-xr-x 150 root root 4096 Jul 28 19:06 ..
-rw-r--r--   1 root root  220 Mar 31  2024 .bash_logout
-rw-r--r--   1 root root 3851 Jul 28 18:47 .bashrc
drwxr-xr-x   2 root root 4096 Jul 28 19:03 inhere
-rw-r--r--   1 root root  807 Mar 31  2024 .profile
```
- I was experimenting and discovered that I can combine flags together. `ls -la` has the same effect as `ls -l -a` according to [Joseph Gefroh](https://jgefroh.medium.com/a-beginners-guide-to-linux-command-line-56a8004e2471)
- Above, you can see that the files `.bashrc` and `.profile` are hidden, but I believe they have nothing to do with completing the Bandit challenge. I think they're hidden to prevent confusion.

## What I Learned

### New Commands/Concepts
1. **Hidden files in Linux**: Files starting with `.` are hidden and require the `-a` flag to be visible
2. **`cd` command**: Changes directories, essential for navigating the file system
3. **Combining command flags**: Flags can be combined for efficiency (e.g., `ls -la` instead of `ls -l -a`)
4. **Directory navigation**: Understanding `.` (current directory) and `..` (parent directory) concepts
5. **Visual cues**: Terminal color coding helps distinguish between files and directories

## Real-World Applications
- **System configuration**: Many important configuration files in Linux are hidden (like `.bashrc`, `.profile`) to keep the home directory clean
- **Security investigations**: Hidden files are commonly used to store malicious scripts or files that attackers don't want easily discovered
- **System administration**: Administrators need to check hidden files when troubleshooting user environments or investigating system issues
- **Software development**: Development tools often store configuration in hidden directories (like `.git`, `.vscode`) that need to be accessed for troubleshooting

## Key Takeaway
Understanding hidden files is fundamental. Both legitimate system files and potentially malicious files can be hidden. The ability to systematically search for and examine hidden files is a core skill that applies to system administration, security analysis, and digital forensics.
