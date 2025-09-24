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









## Challenge Name: Mixing globs
The challenge requires match the files "challenging", "educational" and "pwning" in the directory /challenge/files using multiple globbing.

### Solve
**Flag:** `pwn.college{wgH6pE9EZG2pRRRot0onn9VsCf1.QX1IDO0wyN5AzNzEzW}`

On performing ls command in the /challenge/files there are multiple other files with words "amazing", "delgihtful" etc. The required matches "educational", "challenging" and "pwning" don't have any unique characters or sequences to these three that aren't also present in other files present in the directory. However, "challenging" is the only file that begins with c, "pwning" is the only file that begins with p, and "educational" is the only flag that begins with e. Then a bracket glob can be used to match c,e,p as the first character in the file name followed be anything as there are no other matches beginning with c, e or p. Then the argument would be [cep]*.

```bash
/challenge/run [cep]*
You got it! Here is your flag!
pwn.college{wgH6pE9EZG2pRRRot0onn9VsCf1.QX1IDO0wyN5AzNzEzW}
```

### New Learnings
Multiple globbings can be mixed together according to specifications to find matches. A glob has to also exclude unwanted things instead of just things that are required. (Tried matching with just 'n' first but that came with unwanted matches too).

### References 
-









## Challenge Name: Exclusionary globbing
The challenge requires to find all file matches of file matches that don't start with p, w or n and introduces the ! or ^ characters to exclude characters.

### Solve
**Flag:** `pwn.college{0MfkUIxnq0urIT-KL7l9Oe360Z5.QX2IDO0wyN5AzNzEzW}`

The challenge requires that the file names don't begin with p, w or n so a simple bracket glob with ^ works: [^pwn] and there's no other constrains on file names so following characters can be anything. Full argument would be [^pwn]*.

```bash
/challenge/files$ /challenge/run [^pwn]*
You got it! Here is your flag!
pwn.college{0MfkUIxnq0urIT-KL7l9Oe360Z5.QX2IDO0wyN5AzNzEzW}
```

### New Learnings
! or ^ can be used to carry out exclusionary globbing i.e. avoiding characters that aren't wanted

### References 
-









## Challenge Name: Tab completion
Read (cat) the /challenge/pwncollege file without typing out the file name and using tab completion instead.

### Solve
**Flag:** `pwn.college{s874PsdULRRDHFFEA9iBlHUAZQ1.0FN0EzNxwyN5AzNzEzW}`

Tab completion is used for autocompletion since the directory only contains two files: DESCRIPTION.md and pwncollege, on doing cat /challenge/pwn<TAB> the command autocompletes to cat /challenge/pwncollege and reads the file.

```bash
command 1
command 2
pwn.college{helloworld}
```

### New Learnings
Tab is used for autocompletion and basically helps save time typing out entire names.

### References 
-









## Challenge Name: Multiple options for tab completion
The challenge is to use tab completion to read the file that contains the flag from a directory that contains multiple files with the same starting name. Tab key has to be employed multiple times to list the duplicate options and then find the correct file.

### Solve
**Flag:** `pwn.college{4WM_ag8aEahKaRkX7WD6FDlLS7L.0lN0EzNxwyN5AzNzEzW}`

First, using /challenge/files/p<TAB>, the command gets completed to /challenge/files/pwn and stops completion at the common prefix. On pressing tab a second time all the files that begin with 'pwn' are displayed /challenge/files/p<TAB><TAB>. From there the pwncollege-flag contains the flag.

```bash
cat /challenge/files/pwn<TAB><TAB>
pwn                    pwn-the-planet         pwncollege-flag        pwncollege-flyswatter
pwn-college            pwncollege-family      pwncollege-flamingo    pwncollege-hacking

cat /challenge/files/pwncollege-flag
pwn.college{4WM_ag8aEahKaRkX7WD6FDlLS7L.0lN0EzNxwyN5AzNzEzW}
```

### New Learnings
A tab completion completes as much as it can until it reaches ambiguity with files names and then waits for multiple tabs to list all possible completions. 

### References 
-









# Module Name: Tab completion on commands
The challenge builds on the concept of tab to autocomplete but instead on commands, the challenge requires to autocomplete the pwncollege command to execute the entire command to retrieve the flag.

## Challenge Name
Typing the pwncollege command and pressing the tab key autocompletes the command which gives the flag.

### Solve
**Flag:** `pwn.college{4RtRXkxi4dEa_iRxXxnfc7B5DZ7.0VN0EzNxwyN5AzNzEzW}`


```bash
pwncollege<TAB>
pwncollege-9352
Correct! Here is your flag:
pwn.college{4RtRXkxi4dEa_iRxXxnfc7B5DZ7.0VN0EzNxwyN5AzNzEzW}
```

### New Learnings
Tab completion can be used for paths and commands too.

### References 
-
