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

**Step 1: [What you did first]**
```bash
banditX@bandit:~$ [command you used]
```
- [Explain what the command does in your own words]
- [Explain any flags/options you used and why]
- [Mention if the flag was necessary or just helpful]
- Result: [What happened when you ran this]

**Step 2: [Next action]**
```bash
banditX@bandit:~$ [command you used]
```
- [Your explanation of the command]
- [What the result was]
- [Any notes about following Bandit rules, like not posting passwords]

[Add more steps as needed]

## What I Learned

### New Commands/Concepts
1. `command` [brief description of what it does]
   - [Key flags or options you learned]
2. [Any other commands or concepts]
3. [Broader learning about Linux/security]

## Real-World Applications
- [How this command helps in security work - be specific]
- [Quick research insight about how professionals use this]
- [Your thoughts on the practical applications]

## Key Takeaway
[Your personal reflection on what this level taught you about cybersecurity, hacking, or your own learning journey. This is where your personality and genuine reactions shine through]
