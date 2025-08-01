# [Bandit Level 2 → Level 3](https://overthewire.org/wargames/bandit/bandit3.html)

## Challenge Description
The password for the next level is stored in a file called `--spaces in this filename--` located in the home directory.

Commands you may need to solve this level:
`ls` `cd` `cat` `file` `du` `find`

[Google Search for "spaces in filename"](https://www.google.com/search?q=spaces+in+filename)

## My Experience

### Initial Approach/Struggles
I couldn't read the file because there were spaces in the filename. The `cat` command perceived the filename as separate arguments and parameters when I tried reading `--spaces in this filename--`. Additionally, the double dashes at the beginning made the command think it was an option flag.

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
- It seems like the file is specially named, just like the last level's file which contained the password
- The double dashes at the beginning made `cat` think `--spaces` was a command option, causing an error

**Step 2: Exploring other commands**
I wanted to test the other commands provided by Bandit and see if they would shed any light after trying out `cat` one more time.

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

- `find` searches for files in the directory. The `*` searches for all filenames ([Shotts](https://linuxcommand.org/lc3_lts0050.php))
- `du` estimates the amount of space each file and directory in the current directory uses. However, I used it just to also look up the names of the files. The `-a` flag tells Terminal to ensure every file is estimated. I got this from the [Ubuntu manual](https://manpages.ubuntu.com/manpages/noble/man1/du.1.html)
- Result: The `du` command confirmed the exact filename, and I realized I need to handle the spaces properly

**Step 3: Finding the solution**
```bash
bandit2@bandit:~$ cat '--spaces in this filename--'
cat: unrecognized option '--spaces in this filename--'
Try 'cat --help' for more information.
bandit2@bandit:~$ cat "./--spaces in this filename--"
[password displayed]
```

- Adding single quotation marks at the beginning and end of the file didn't work
- By a stroke of luck, I used double quotation marks instead and got the password to the next level. Honestly, I made a crazy connection to Java programming; a `String` literal uses quotation marks, and I wondered if putting double quotation marks would work. Java is everywhere!

## What I Learned

### New Commands/Concepts
1. **Handling filenames with spaces and special characters**: Use double quotes combined with `./` to treat the entire filename as one argument and avoid option parsing
2. **`find` command**: Searches for files in directories, but struggles with spaces and special characters in filenames without proper quoting
3. **`du` command**: Shows disk usage, but the `-a` flag is useful for listing all files including their exact names
4. **Command parsing**: Linux commands split arguments by spaces, and double dashes are interpreted as options, so filenames with both need special handling

## Real-World Applications
- **System administration**: Many files in real systems have spaces in their names (especially in Windows environments or user-created files)
- **Scripting and automation**: When writing security scripts, you must handle filenames with spaces properly or risk missing important files
- **Digital forensics**: Investigators often encounter files with unusual names (including spaces) that suspects use to try hiding evidence
- **Log analysis**: Log files and configuration files sometimes have spaces in their names, requiring proper syntax to examine them

## Key Takeaway
Spaces in filenames are more common than I initially thought, and learning to handle them properly is essential for any cybersecurity work. This level taught me that the command line treats spaces as argument separators, but proper quoting (with double quotes) tells the shell to treat the entire string as one filename. My programming background actually helped me make the connection - just like string literals in code, filenames with special characters need to be properly delimited.
