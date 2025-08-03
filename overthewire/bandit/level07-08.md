# [Bandit Level 6 → Level 7](https://overthewire.org/wargames/bandit/bandit7.html)

## Challenge Description
The password for the next level is stored somewhere on the server and has all of the following properties:

- owned by user bandit7
- owned by group bandit6
- 33 bytes in size

Commands you may need to solve this level:
`ls` `cd` `cat` `file` `du` `find` `grep`

## My Experience

### Initial Approach/Struggles
Understanding the challenge description gave me a headache. When I first tried to find the file in the directory I was currently in, there were no files that matched. The key phrase "somewhere on the server" was confusing.

I realized I wasn't just looking in one directory anymore, but potentially anywhere on the entire system. Additionally, Bandit recommended using `grep`, which turned out to be a red herring since I didn't end up needing it for the main solution.

### Solution Process

**Step 1: Check the current directory**
```bash
bandit6@bandit:~$ ls -las
total 20
4 drwxr-xr-x   2 root root 4096 Jul 28 19:03 .
4 drwxr-xr-x 150 root root 4096 Jul 28 19:06 ..
4 -rw-r--r--   1 root root  220 Mar 31  2024 .bash_logout
4 -rw-r--r--   1 root root 3851 Jul 28 18:47 .bashrc
4 -rw-r--r--   1 root root  807 Mar 31  2024 .profile
```
- As expected, there were no files in my home directory that matched the criteria
- This confirmed I needed to search beyond just my current location

**Step 2: Understanding the scope - searching the entire server**
```bash
bandit6@bandit:~$ find . -type f
./.profile
./.bashrc
./.bash_logout
bandit6@bandit:~$ find / -type f
/opt/radare2/configure.hook
/opt/radare2/autogen.sh
/opt/radare2/config-user.mk.acr
[thousands of files listed]
```
- I realized that I was working in a subdirectory, not at the root of the server
- The challenge meant searching the entire OverTheWire server, not just my user directory
- Using `find /` searches from the root directory of the entire system

**Step 3: Apply the specific criteria**
```bash
bandit6@bandit:~$ find / -type f -user bandit7 -group bandit6 -size 33c
find: '/sys/kernel/tracing': Permission denied
find: '/sys/kernel/debug': Permission denied
find: '/sys/fs/pstore': Permission denied
find: '/sys/fs/bpf': Permission denied
find: '/tmp': Permission denied
[many more "Permission denied" errors]
```
- When I specified the exact criteria from the challenge, I got lots of permission errors
- These errors cluttered the output and made it hard to see any actual results

**Step 4: Filter out permission errors**
```bash
bandit6@bandit:~$ find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
/var/lib/dpkg/info/bandit7.password
bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
[password displayed]
```
- I had to Google how to remove the "Permission denied" messages
- The solution was adding `2>/dev/null` to the end of the command
- This redirects error messages (stderr) to `/dev/null`, which essentially discards them

## What I Learned

### New Commands/Concepts
1. **Server-wide file searching**: Using `find /` searches the entire server from the root directory
2. **File ownership criteria**: The `-user` and `-group` flags let you search by file ownership
3. **Error redirection**: `2>/dev/null` hides error messages by redirecting them to the null device
4. **Standard streams**: Understanding stdin (0), stdout (1), and stderr (2) and how to redirect them
5. **OverTheWire.org**: Realized that OverTheWire challenges can span the entire server, not just user directories. I can not trust Bandit.

### Key Technical Concepts
- **Standard streams**: 
  - `0` = stdin (standard input)
  - `1` = stdout (standard output - successful results)
  - `2` = stderr (standard error output - error messages)
- **Redirection**: The `>` symbol redirects output to a file or device
- **`/dev/null`**: A special device that discards everything sent to it (like a digital trash can)

## Real-World Applications
- **System administration**: Searching for files by ownership is crucial when investigating user activities or cleaning up after departed employees
- **Security auditing**: Finding files owned by specific users or groups helps identify potential privilege escalation or unauthorized access
- **Digital forensics**: Investigators often need to locate files across entire systems based on specific criteria like ownership, size, or timestamps
- **Compliance monitoring**: Organizations need to track files owned by certain users or groups for regulatory compliance
- **Error handling in scripts**: Using redirection to manage error output is essential for creating clean, professional automation scripts

## Key Takeaway
This level taught me that cybersecurity work often involves searching through vast amounts of data systematically. Learning to construct precise search queries and handle error output professionally is essential when working with large systems. The skills I learned here about file ownership, system-wide searching, and error management will be fundamental as I progress to more security challenges.
