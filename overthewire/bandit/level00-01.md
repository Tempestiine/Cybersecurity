# [Bandit Level 0 → Level 1](https://overthewire.org/wargames/bandit/bandit1.html)

## Challenge Description
The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

Commands you may need to solve this level

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

- `ls` lists files in the current directory.
- The `-l` after `ls` is known as a flag, a special modifier that alters the behavior of commands in my own words, that changes `ls` to instead display files in long format, displaying detailed information of each file. If you type only `ls`, only the names of files appear, no extra information.
- Result: I found one file named `readme`.

**Step 2: Read the file**
```bash
banditX@bandit:~$ [command used]
```
- [Explanation]
- [Result]

[Add more steps as needed]

## What I Learned

### New Commands/Concepts
- **`command`**: [What it does and key options you learned]
- **Concept**: [Any new Linux/security concept you discovered]

### Mistakes & Lessons
- [What didn't work and why]
- [How I figured out the correct approach]

## Real-World Applications

### In Cybersecurity
- **[Security area]**: [How this technique applies to real security work]
- **[Another area]**: [Another practical application]

### Practical Uses
- [How system administrators would use this]
- [How this helps in troubleshooting or automation]

## How I'll Use This Again
- [When I'd use these commands in future challenges]
- [What patterns or approaches I'll remember]
- [How this builds toward more advanced techniques]

## Key Takeaway
[One main lesson that summarizes what made this level valuable for my cybersecurity learning]

---

**Tools Used:** [List main commands/tools]  
**Difficulty:** [Personal rating and why]  
**Time Spent:** [How long it took]
