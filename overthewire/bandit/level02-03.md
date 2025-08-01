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
```bash
bandit2@bandit:~$ du -a
4       ./.profile
4       ./--spaces in this filename--
4       ./.bashrc
4       ./.bash_logout
20      .
```
--

- `find` searches for any files in the directory. The `*` searches for all filenames. [Shotts](https://linuxcommand.org/lc3_lts0050.php).
- `du` estimates the amount of space each file and directory in the current directory uses. However, I used it just to also look up the names of the files. The `-a` flag tells Terminal to ensure every file is estimated. I got this from the [Ubuntu manual](https://manpages.ubuntu.com/manpages/noble/man1/du.1.html)
- Result: In order to read the file I want, it seems like I need to add special characters at the beginning and end of it.

**Step 2: One More Time**
```bash
bandit2@bandit:~$ cat '--spaces in this filename--'
cat: unrecognized option '--spaces in this filename--'
Try 'cat --help' for more information.
bandit2@bandit:~$ cat "./--spaces in this filename--"
```

- Adding single quotation marks at the beginning and end of the file did nothing
- By a stroke of luck, I used double quotation marks instead and got the password to the next level. Honestly, I made a crazy connection to Java programming; A `String` literal uses quotations marks, and I wondered if I putting double quotation marks would work. Java is everywhere
 
## What I Learned

### New Commands/Concepts
??
'find', 'du' 'du -a'
1. I can read files with spaces using double quotation marks.
2. I can accurately search through files with the 'find' command
   

## Real-World Applications
?

## Key Takeaway
?
