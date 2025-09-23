# Module Name: File Globbing

## Challenge Name: Matching with *
The challenge requires the usage of wildcard * to change directories and run the flag program.

### Solve
**Flag:** `pwn.college{otsfbUBxiAmiVlnsGrB6gPRKyns.QXxIDO0wyN5AzNzEzW}`

The challenge requires the argument of cd to be 4 or less characters therefore the requirement is to find a pattern than can expand to challenge. Then, /c* means a path starting with /c followed by anything, since the only match is challenge, the full expanded path is /challenge for /c*. Then run /challenge/run.
```bash
cd /c*
/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{otsfbUBxiAmiVlnsGrB6gPRKyns.QXxIDO0wyN5AzNzEzW}
```

### New Learnings
This challenge introduces the * glob character, it acts as a wildcard character that matches any sequence of characters, it can be used to shorten path names or find all possible matches

### References 
-
