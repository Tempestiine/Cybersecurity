# [Bandit Level 7 → Level 8](https://overthewire.org/wargames/bandit/bandit8.html)

## Challenge Description
The password for the next level is stored in the file `data.txt` next to the word `millionth`

Commands you may need to solve this level
`man` `grep` `sort` `uniq` `strings` `base64` `tr` `tar` `gzip` `bzip2` `xxd`

## My Experience

### Initial Approach/Struggles
This challenge was a breath of fresh air, compared to the last one. I scanned the data file, searching for the word `millionth`, and I found the password.

### Solution Process

**Step 1: Read the data file**
```bash
bandit7@bandit:~$ man strings
bandit7@bandit:~$ man grep
bandit7@bandit:~$ ls
data.txt
bandit7@bandit:~$ strings data.txt | grep "millionth"
millionth       [password displayed]
```

- `strings` is a more complex version of `cat`. While `cat` prints out everything, `strings` only outputs printable characters in a file. Because many data files do not have printable characters, `strings` is more useful.
- `|` is called a pipe. Imagine an assembly line, "a series of workers and machines in a factory," all connected by conveyor belts. `strings data.txt` is the first operation or machine, and the output of the first machine is transfered to the second operation or command `grep "millionth". Essentially, I'm telling Linux to gather printable characters from the data file and search for the word "millionth" within that selected population. ([Ken Hess](https://www.redhat.com/en/blog/pipes-command-line-linux))
- As a result, the password was displayed next to the word `millionth`.

## What I Learned

### New Commands/Concepts
strings reads files
grep scans files (but is it a new command?) It's best used with piping that's for sure.
passwords can be hidden in data files
piping allows me to be multifaceted with multiple commands?

## Real-World Applications
what i imagine
people can hide sensitive information within innocent looking files
things can be encrypted or disguised in said files
people have to be wary of what they download or install because files can contain anything
investigators have to search everything, including files that appear unrelated.

## Key Takeaway ?
Data files are now on my radar.
cybersecurity involves legal breaches of privacy and thorough scanning?

