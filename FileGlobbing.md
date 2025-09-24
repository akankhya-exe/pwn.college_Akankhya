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










## Challenge Name: Matching paths with []
The goal is to run /challenge/run with an argument that uses the [] glob to find file_a, file_b, file_s, file_h using absolute path. The single argument must expand to the full absolute paths of those four specific files.

### Solve
**Flag:** `pwn.college{YWA46pY4nxfKFuA55IHDANo2Zui.QX0IDO0wyN5AzNzEzW}`

The command needs to receive the entire absolute path like /challenge/files/file_a, for all four files the common part is /challenge/files/file_ and the variable part is the single character at the end. [] glob can be used to specify the subset of a,b,s,h in the path.

```bash
/challenge/run /challenge/files/file_[bash]
You got it! Here is your flag!
pwn.college{YWA46pY4nxfKFuA55IHDANo2Zui.QX0IDO0wyN5AzNzEzW}
```

### New Learnings
Globbing works on entire paths, not just for file names or relative paths (in the current directory), [] can be used to implement globbing in file paths

### References 
-









## Challenge Name: Multiple globs
The challenge introduces the concept of multiple globbing; multiple globs in a single world. The challenge requires to run the command /challenge/run with an argument that covers every word that has the letter p in it.

### Solve
**Flag:** `pwn.college{IELETWjZ-iB9tyECvKvk3OdfO3s.0lM3kjNxwyN5AzNzEzW}`

The question states there must be only three characters in the argument to cover every word that contains the letter p which means there can be anything before and after p, including nothing, to search for all possible matches and any number of characters, the * glob is appopriate. For any word with p in it the argument would be: *p* to cover any characters before and after it so the entire command is /challenge/run *p*.

```bash
/challenge/run *p*
You got it! Here is your flag!
pwn.college{IELETWjZ-iB9tyECvKvk3OdfO3s.0lM3kjNxwyN5AzNzEzW}
```

### New Learnings
There can be multiple wildcards in a single glob to create more wide-ranging search criterias, also the "contains" pattern can be solved by using the * multiple globbing process.

### References 
-
