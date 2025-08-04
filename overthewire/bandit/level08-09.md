# [Bandit Level 7 → Level 8](https://overthewire.org/wargames/bandit/bandit9.html)

## Challenge Description
The password for the next level is stored in the file data.txt and is the only line of text that occurs only once

Commands you may need to solve this level:
`man` `grep` `sort` `uniq` `strings` `base64` `tr` `tar` `gzip` `bzip2` `xxd`

## My Experience

### Initial Approach/Struggles
This challenge was a bit hard because `uniq` wants a specific kind of input.

### Solution Process

**Step 1: Explore the available tools and examine the file**

```bash
bandit8@bandit:~$ ls
data.txt
bandit8@bandit:~$ man uniq
bandit8@bandit:~$ strings data.txt |  uniq -u
XufULFiOZWAHsAxw0bIUQGrZZFyBRlZL
r9fBFHH41cMCOBt7J0FzTMu6qhmyg1ju
ZO25yUpC8UtUCb00m8nV0IOd8jAMVbKG
[fake passwords]
```

```bash
bandit8@bandit:~$ man sort
bandit8@bandit:~$ strings data.txt | sort -u
066lBi8GrHITCQmvVAgMOdGGXrXhYmmO
1nd1ZEdrz8EVgTAhESS7YsDyI1E4PtOc
20XnpTGhJBb02GfFqE4sjppp3x8Blgm9
[fake passwords]
```

- `uniq` identifies unique lines of code in text. I fed printable characters to `uniq -u`, but the command didn't work the way I thought it would.
- Checking sort, I saw that it had the `-u` and `--unique` flag option, and I thought it would sort and output unique lines for me; however, I got an identical result as `uniq -u`. Reading the Ubuntu manual page for `uniq`, I discovered that I may need "to sort the input first..."

```bash
bandit8@bandit:~$ strings data.txt | sort | uniq -u
[password displayed]
```


## What I Learned (Possibly?)

### New Commands/Concepts
1. How to find unique text
2. How to use sort

## Real-World Applications?
looking for unique data for data analysis?
looking for unique system entries or people using networks and stuff like that?
maybe, you want to sort programs by how much cpu or gpu memory they take up and you want to see the biggest stuff first
maybe you sort by file type and size.
maybe hackers have multiple files that are identical to slow down your time, so you use uniq to find distinct files and not redudant ones.

## Key Takeaway
??
