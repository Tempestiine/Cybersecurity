# [Bandit Level 6 → Level 7](https://overthewire.org/wargames/bandit/bandit6.html)

## Challenge Description
The password for the next level is stored somewhere on the server and has all of the following properties:

- owned by user bandit7
- owned by group bandit6
- 33 bytes in size

Commands you may need to solve this level:
`ls` `cd` `cat` `file` `du` `find` `grep`

## My Experience

### Initial Approach/Struggles
Understanding the Challenge Description gave me a headache. When I first tried to find the file in the directory that I was situated in, there were no files. In addition, Bandit recommended the use of `grep`, which now seems like a red herring because I didn't use it.

### Solution Process

**Step 1: Find the right file**

```bash
bandit6@bandit:~$ ls -las
total 20
4 drwxr-xr-x   2 root root 4096 Jul 28 19:03 .
4 drwxr-xr-x 150 root root 4096 Jul 28 19:06 ..
4 -rw-r--r--   1 root root  220 Mar 31  2024 .bash_logout
4 -rw-r--r--   1 root root 3851 Jul 28 18:47 .bashrc
4 -rw-r--r--   1 root root  807 Mar 31  2024 .profile
```

- Above, there are no files that are connected with this challenge.
- Afterward, I messed around with `grep`. `grep` is a sophisticated version of `find` which insteads looks for specific patterns of data or information inside files. However, the challenge description didn't provide a pattern that I was looking for. It only provided file permissions.
- At this point, I searched on Google: "How to navigate and read files on servers in Linux Command Line with find?" and hints on the Bandit Level
- This sounds fourth-dimensional or meta. What I learned is that, apparently, when you're starting out in Bandit, you're set in a subdirectory. You're not even at the root! overthewire is like one big computer, and the home directory has all of its challenges: bandit, leviathan, and narnia. And you're supposed to find the password located somewhere on the server or machine?? [explain this better please] or is the home directory the users?? I'm lost.
- I need to use `find /` to use the root directory of overthewirelabs.org? oml

**Step 2: Find the right file**
```bash
bandit6@bandit:~$ find . -type f
./.profile
./.bashrc
./.bash_logout
bandit6@bandit:~$ find / -type f
/opt/radare2/configure.hook
/opt/radare2/autogen.sh
/opt/radare2/config-user.mk.acr
/opt/radare2/binr/preload/libr2.c
/opt/radare2/binr/preload/trap-darwin-x86-32.asm
/opt/radare2/binr/preload/demo.c
/opt/radare2/binr/preload/alloc.c
[thousands of more, various files]
```

```bash
bandit6@bandit:~$ find / -type f -user bandit7 -group bandit6 -size 33c
find: ‘/sys/kernel/tracing’: Permission denied
find: ‘/sys/kernel/debug’: Permission denied
find: ‘/sys/fs/pstore’: Permission denied
find: ‘/sys/fs/bpf’: Permission denied
find: ‘/tmp’: Permission denied
find: ‘/run/udisks2’: Permission denied
[a bunch of files with "Permission denied"]
bandit6@bandit:~$ find / -type f -user bandit7 -group bandit6 -size 33c | grep -v "Permission denied"
[nearly identical output as previous command]
```

- Looking in the root directory worked, but I had a bunch of unnessary files.
- When I specified it to what the challenge description wanted, I couldn't access a lot of the files. I tried using `-v` flag to use the inverse of `grep` and to instead choose files without "Permission denied", but that didn't work.
- I had to do a google search to find the answer on how to remove all of the Permissions denied.
- Apparently, I need to add ```2>/dev/null``` to the end of the Linux command.

---

Search up how to add tables in markdown
0	stdin	Standard input
1	stdout	Standard output
2	stderr	Standard error output

successful results to stdout (1)

error messages (like "Permission denied") to stderr (2)

 and the arrow `>` means...

In shell scripting (like Bash), the > symbol redirects output of a command to a file or another place, instead of printing it to the screen (your terminal).

/dev/null is a special device that deletes everything inside of it. Like a garbage collector. Haha java pun

---

**Step 3: Get the Password**
```bash
bandit6@bandit:/var/lib/dpkg/info$ find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
/var/lib/dpkg/info/bandit7.password
bandit6@bandit:/var/lib/dpkg/info$ cat /var/lib/dpkg/info/bandit7.password
[password displayed]
```

## What I Learned

### New Commands/Concepts?
1. How to use grep
2. how to use find and how to access root directory from subdirectory
3. what standard input, output, and errors mean and their differences
4. how to use redirection.

## Real-World Applications?
I imagine you use grep to find specific text in files like passwords if you're hacking.
If you're looking for anything, sometimes, you need to look in the root directory?
In hacking, you're bound to encounter errors. Don't let them cloud up your screen.
passwords can be hidden anywhere, even in the most unconventional places.

## Key Takeaway
you need to check everything and everywhere. do not trust bandit. idk. look at reddit and quora.
