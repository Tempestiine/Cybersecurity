# [Bandit Level 01 → Level 02](https://overthewire.org/wargames/bandit/bandit2.html)

## Challenge Description
The password for the next level is stored in a file called - located in the home directory

Commands you may need to solve this level:

`ls` `cd` `cat` `file` `du` `find`

[Google Search for "dashed filename"](https://www.google.com/search?q=dashed+filename)

[Advanced Bash-scripting Guide - Chapter 3 - Special Characters](https://linux.die.net/abs-guide/special-chars.html)

## My Experience

### Initial Approach/Struggles

Beforehand, I was actually struggling with submitting a password to access this level. To save their resources, Bandit will not allow me to use `ssh` from the bandit0 account to connect to bandit1. Bandit told me to log out. I made a text file to contain my passwords to the bandit accounts and pasted the bandit1 password inside Kali Linux. When I pressed `ctrl` and `D`, I logged out of bandit0 and stayed in the terminal.

At first, I thought no files existed. However, looking at Bandit, I deduced that there's a file literally named `-`, so I tried reading it.

### Solution Process

**Step 1: Read the file**

```bash
bandit1@bandit:~$ ls
-
bandit1@bandit:~$ cat -
^C
bandit1@bandit:~$ cat "-"
^C
```
- `ls` reveals the contents of a director
- `cat` reads text from a file directly on terminal
- `^C` is a signal to terminal to terminate a process. Likewise, in Java and Python, `break` terminates a process. This is created by pressing both `ctrl` and `D`
- I used `^C` because I think there was something wrong with Terminal. I was stuck using the command, and Terminal seemed to have paused itself.
- Result: I did a Google search on how to read "dashed filenames."

**Step 2: Try Again**

```bash
bandit1@bandit:~$ cat ./-
```
- According to [Shotts](https://linuxcommand.org/lc3_lts0020.php), "the `.` notation refers to the working directory itself", and when running most commands, "./" is implied at the beginning.
- Basically, the `.` tells Terminal to look at the directory we are currently located, which is supposed to seem arbitrary but has an important use. Likewise, in Java programming, some constructors implicity call `super()` first while instance variables and called instance methods within instance methods have `this.` implicitly added at the beginning.
- I ran the command above and obtained the password to the next level.

## What I Learned

### New Commands/Concepts
1. I have to rework the `cat` command when trying to read files with special characters.
2. Some commands implicitly add `./` at the beginning.

## Real-World Applications
- ? N/A?

## Key Takeaway
- Naming a file with special characters does not protect hackers from accessing private content.
