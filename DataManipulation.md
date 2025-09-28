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
The flag present in /challenge/run is in the format of column 1: random number and column 2: actual flag character spread out over multiple lines, the goal is to extract the flag characters and put them all together to retrirve the full flag.

### Solve
**Flag:** `pwn.college{AsuZkmgsWfO6HIOKSXgkuFRErNt.01NxEzNxwyN5AzNzEzW}`

As seen in the cat command output and in the question, the random numbers are a distraction and the actual characters are only in the second column, to extract data from a particular column the cut command can be used. The cut command has two arguments:
-d : specifies the delimiter; how the columns are seperated
-f : the field number to be extracted from
Here, the columns are separated by spaces so the delimiter is " " [$RANDOM <SPACE> $C] and the file column number is 2 as given in the question. The cut arguments are -d " " -f 2.
Next is taking out all the newlines which can be done by tr -d.
Putting everything together: /challenge/run | cut -d " " -f 2 | tr -d "\n|

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
cut tool is used to extract vertical columns of text, it has two main arguments -d the delimiter and -f the column or field number, processing column based data

### References 
-









## Challenge Name: Sorting data
/challenge/flags.txt contains a 100 flags with the real flag hidden in it. If sorted in alphabetical order, the real flag comes at the very end, the goal is to retrieve the real flag by using sorting.

### Solve
**Flag:** `pwn.college{Yhk26-DQq_YF6p1AHDCGuZayzes.0FM0MDOxwyN5AzNzEzW}`

Since when sorting in alphabetical order the real flag comes at the end, the file needs to be sorted in reverse. sort -r command can be used to sort in reverse order. The command is simply sort -r /challenge/flags.txt and take the first output as it's the last flag in normal alphabetical order.

```bash
sort -r /challenge/flags.txt
pwn.college{Yhk26-DQq_YF6p1AHDCGuZayzes.0FM0MDOxwyN5AzNzEzW}
pwn.college{Yhk26-DQq_YF6p1AHDCGuZayzes.0FM0MDOxwyN5AzNzEzW}
pwn.college{Yhk26-DQq_YF6p1AHDCGuZayzes.0FM0MDOxwyN5AyNzEzW}
pwn.college{Yhk26-DQq_YF6p1AHDCGtZayzes.0FM0MDOxwyN5AzNzEzW}
...
```

### New Learnings
Data can be sorted using the sort command which has the arguments -r (reverse), -n (numeric), -u (remove duplicates), -R (random), the default is alphabetic sorting.

### References 
-
