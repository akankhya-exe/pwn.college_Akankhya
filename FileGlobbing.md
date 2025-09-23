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









## Challenge Name: Matching with ?
This challenge requires to switch directories using the glob ? character which is like the * character but instead only matches one character instead of any number. 
### Solve
**Flag:** `pwn.college{helloworld}`

According to the question, c's and l's must be replaced in cd/challenge by the ? glob character which only matches one character so the command would be cd /?ha??enge which matches with the only directory /challenge.

```bash
cd /?ha??enge
/challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{U6wxfggTGdSqrHo-qxAWFxNO2gN.QXyIDO0wyN5AzNzEzW}
```

### New Learnings
? is another glob character that performs the same wildcard function except it matches one character at a time instead of any number of characters like the * character

### References 
-









## Challenge Name: Matching with []
The goal is to use glob [] with a subset of characters to match with four files file_a, file_b, file_s, file_h with the /challenge/run command

### Solve
**Flag:** `pwn.college{oPpn5YSqWRL6G9LIDmQl2WObh35.QXzIDO0wyN5AzNzEzW}`

The only part that differs out of the four required files are the last characters, i.e., b, a, s, h. The [] glob is made to match any specific character from the subset provided to it which works here best.
(* or ? would match with every single file with a letter after file_ and not just the required four files). The required subset is bash, hence the command is /challenge/run file_[bash]

```bash
cd /challenge/files
/challenge/run file_[bash]
You got it! Here is your flag!
pwn.college{oPpn5YSqWRL6G9LIDmQl2WObh35.QXzIDO0wyN5AzNzEzW}
```

### New Learnings
[] is used to match any one character from the subset provided to it, this can be used for preciison matching rather than * and ? that match wtih any character

### References 
-

