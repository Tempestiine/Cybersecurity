# [Bandit Level 0 → Level 1](https://overthewire.org/wargames/bandit/bandit1.html)

## Challenge Description
The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

Commands you may need to solve this level:

`ls` `cd` `cat` `file` `du` `find`

TIP: Create a file for notes and passwords on your local machine!

Passwords for levels are not saved automatically. If you do not save them yourself, you will need to start over from bandit0.

Passwords also occasionally change. It is recommended to take notes on how to solve each challenge. As levels get more challenging, detailed notes are useful to return to where you left off, reference for later problems, or help others after you’ve completed the challenge.

## My Experience

### Initial Approach/Struggles

The real struggle wasn't navigating this level but understanding how to use commands in Terminal effectively. Frankly, I'm a beginner. I was confused by the command syntax and how arguments worked in Terminal. The Ubuntu documentation provided on the Bandit website gave me a headache. Connecting to OverTheWire initially felt overwhelming. The Wikipedia page helped clarify some concepts, but I didn't fully grasp the semantics of how to type and use commands.

Fortunately, I found [linuxcommand.org](https://linuxcommand.org/) (copyright William E. Shotts, Jr.), which explained Linux commands in a way that finally made sense.

### Solution Process

**Step 1: List directory contents**

```bash
bandit0@bandit:~$ ls -l
```

- `ls` lists files in the current directory
- The `-l` after `ls` is known as a flag, a special modifier that alters the behavior of commands in my own words, that changes `ls` to instead display files in long format, displaying detailed information of each file. If you type only `ls`, only the names of files appear, no extra information. I don't think adding the flag was necessary
- Result: I found one file named `readme`

**Step 2: Read the file**

```bash
bandit0@bandit:~$ cat readme
```
- `cat` reads and displays the contents of a file
- The file contained a welcome message and the password for the next level
- Because I am following the rules from Bandit, I can't and won't post the actual password

## What I Learned

### New Commands/Concepts

1. `ls` lists contents in a directory
   - `-l` flag provides detailed file information
2. `cat` displays file contents directly in terminal
3. I learned how to navigate and read files in the Linux system

## Real-World Applications

- `ls -l` is important for examining file permissions during security assessments. I bet this command is great to ensure whether a file is secure and private or not.
- `cat` is great for quickly viewing files. Using a quick Google search, I see a few forums of people using `cat` to prevent the modification of files. That's pretty smart.

## Key Takeaway

I'm scared of how these small commands are very powerful. I have not scraped the surface of ethical hacking, but I feel vulnerable. Moreover, I was more surprised that I can do these commands on every computers inside my home. I bet I can apply these commands anywhere, but I'll choose to use the skills in a legal, ethical manner.
