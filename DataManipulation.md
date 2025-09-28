# Module Name: Data Manipulation

## Challenge Name: Translating characters
The flag has been case swapped (a is A and A is a), the goal is to use tr to get the correctly case swapped flag.

### Solve
**Flag:** `pwn.college{o4UGj6CYWZs_dY6vGNFEhilUwvO.01MxEzNxwyN5AzNzEzW}`

The problem is that the characters are in the wrong case, tr is used to manipulate characters, it takes two arguments: a "from" and a "to" set. Here: translate from a-z to A-Z and from A-Z to a-z. The entire from set is a-zA-Z and the entire to set is A-Za-z.
The output of /challenge/run needs to fed into tr to change the case so a pipeline must be used: /challenge/run | tr (from) (to).

```bash
/challenge/run | tr 'a-zA-Z' 'A-Za-z'
yOUR CASE-SWAPPED FLAG:
pwn.college{o4UGj6CYWZs_dY6vGNFEhilUwvO.01MxEzNxwyN5AzNzEzW}
```

### New Learnings
tr can be used to manipulate characters in a character stream, tr can operate on character ranges like a-z (typed everything out manually first which worked but range is a lot easier), tr can be used to edit characters.

### References 
-









## Challenge Name: Deleting characters
The /challenge/run file has unnecessary characters like % and ^ that need to be deleted, this challenge introduces deleting using tr.

### Solve
**Flag:** `pwn.college{MTZydbrxK5UQtLzsQezHqnqCM_E.0FNxEzNxwyN5AzNzEzW}`

tr -d <character set to delete> can be used to delete unwanted characters from a character stream. Here, since ^ and % needs to be deleted, the unwanted set is '^%', putting it in the argument for tr and piping /challenge/run's output to tr:
/challenge/run | tr -d '^%'

```bash
/challenge/run | tr -d '^%'
Your character-stuffed flag:
pwn.college{MTZydbrxK5UQtLzsQezHqnqCM_E.0FNxEzNxwyN5AzNzEzW}
```

### New Learnings
tr -d <set> can be used to delete characters from a stream where <set> includes unwanted characters.

### References 
-









## Challenge Name: Deleting newlines
The flag has been split into different lines, the goal is to delete newline characters and retrieve the flag using escape sequence.

### Solve
**Flag:** `pwn.college{4iAhBzZvtgEY_lsYe9Kv1U7eI2a.0VNxEzNxwyN5AzNzEzW}`

To delete a character /challenge/run output is piped into tr -d <to be deleted character set>, since newline is the Enter key which has a different meaning to the shell, an escape sequence character \n has to be used
enclosed in quotes to symbolize the actual chracter. Putting it all together: /challenge/run | tr -d "\n"

```bash
/challenge/run | tr -d "\n"
Your line-split flag: pwn.college{4iAhBzZvtgEY_lsYe9Kv1U7eI2a.0VNxEzNxwyN5AzNzEzW}
```

### New Learnings
Some sequences like Tab, Enter etc must be specifided using \ escape sequences in order to use them as characters.

### References 
-









## Challenge Name: Extracting the first lines with head
The flag is contained in seperate lines in the /challenge/pwn file with thousands of other irrelevant lines too, the goal is to only output the first 7 lines (using head -n) and pipe it again into /challenge/college.
### Solve
**Flag:** `pwn.college{helloworld}`

Since only the FIRST FEW (first few = head command) lines to be outputted, the head command can be used (7 lines specifically) with /challenge/pwn output as piped input, which is again required to be piped into /challenge/college.

```bash
/challenge/pwn | head -n 7 | /challenge/college
Congratulations, you piped the right codes!
pwn.college{8qMVr2uq81S5B2L2kk3FEibNd6N.0lNxEzNxwyN5AzNzEzW}
```

### New Learnings
head -n command is used to grab the first few lines of a file, by default n=10.

### References 
-









## Challenge Name: Extracting specific sections of text
Add challenge description here

### Solve
**Flag:** `pwn.college{AsuZkmgsWfO6HIOKSXgkuFRErNt.01NxEzNxwyN5AzNzEzW}`

type in your solve and your thought process behind solving the challenge. Include as much as info as possible. Use triple ticks for any bash commands and output you type on the terminal.

```bash
cat /challenge/run
#!/opt/pwn.college/bash

cat /flag | while IFS= read -n1 C; do
    [ -n "$C" ] && echo "$RANDOM $C"
done

/challenge/run | cut -d ' ' -f2 | tr -d '\n'
pwn.college{AsuZkmgsWfO6HIOKSXgkuFRErNt.01NxEzNxwyN5AzNzEzW}
```

### New Learnings
Brief note on what you learned from the challenge

### References 
Add any references or videos you used while solving the challenge.
