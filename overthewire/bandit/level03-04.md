# [Bandit Level 3 → Level 4](https://overthewire.org/wargames/bandit/bandit4.html)

## Challenge Description
The password for the next level is stored in a hidden file in the inhere directory.

Commands you may need to solve this level:

`ls` `cd` `cat` `file` `du` `find`

## My Experience

### Initial Approach/Struggles
This challenge was pretty straightforward.

### Solution Process

**Step 1: Travel to the `inhere` directory**

```bash
bandit3@bandit:~$ ls -l
total 4
drwxr-xr-x 2 root root 4096 Jul 28 19:03 inhere
bandit3@bandit:~$ cd inhere
bandit3@bandit:~/inhere$ ls
bandit3@bandit:~/inhere$ ls -l
total 0
```

- `cd` transfers the user to a directory. In this case, I moved towards the `inhere` directory
- Using `ls -l` won't work. As you can see above, the command doesn't reveal any hidden files.

**Step 2: Access the hidden file**

```bash
bandit3@bandit:~/inhere$ ls -a
.  ..  ...Hiding-From-You
bandit3@bandit:~/inhere$ cat "./...Hiding-From-You"
[password]
```

- I tried the flag `-a` because I wanted Terminal to consider all possible files
- The `-a` flag tells Terminal to not ignore entries starting with `.`
- On my screen, in Kali Linux and in Terminal, I noticed that directories have a bold, blue font while files are in plain white text. I noticed that `.` is a directory, which is the current directory. Above, the `..` actually refers to the parent directory, the place before I did `cd inhere`. This is handy for discerning what is a directory and what is a file name.

```bash
bandit3@bandit:~$ ls -l -a
total 24
drwxr-xr-x   3 root root 4096 Jul 28 19:03 .
drwxr-xr-x 150 root root 4096 Jul 28 19:06 ..
-rw-r--r--   1 root root  220 Mar 31  2024 .bash_logout
-rw-r--r--   1 root root 3851 Jul 28 18:47 .bashrc
drwxr-xr-x   2 root root 4096 Jul 28 19:03 inhere
-rw-r--r--   1 root root  807 Mar 31  2024 .profile
```

- I was messing around, and I noticed that I can combine flags together. `ls -la` has the same effect according to [Joseph Gefroh](https://jgefroh.medium.com/a-beginners-guide-to-linux-command-line-56a8004e2471).

## What I Learned

### New Commands/Concepts
1. **Locating hidden files**: `ls -a` reveals files that can not be accessed with only `ls`
2. **Combining flag options**: For effciency, I can combine flags in order to see the kind of information I want. ???

## Real-World Applications
- **System administration**: Many files in real systems have spaces in their names (especially in Windows environments or user-created files)
- **Scripting and automation**: When writing security scripts, you must handle filenames with spaces properly or risk missing important files
- **Digital forensics**: Investigators often encounter files with unusual names (including spaces) that suspects use to try hiding evidence
- **Log analysis**: Log files and configuration files sometimes have spaces in their names, requiring proper syntax to examine them

## Key Takeaway
From background experience, many people use spaces in filenames, and they don't think like an expert in Cybersecurity or like a hacker. Spaces in filenames are more common, and learning to handle them properly is essential for any cybersecurity work.
