# Module Name: Practicing Piping

## Challenge Name: Redirecting output
The requirement of the challenge is to produce the output PWN and save this output to a file named COLLEGE by using output redirection.

### Solve
**Flag:** `pwn.college{kXjUAnCZxp95LR-L4RlqV0T77_C.QX0YTN0wyN5AzNzEzW}`

The output is PWN and needs to be redirected to the COLLEGE file destination, so the redictor command works as PWN > COLLEGE, the file COLLEGE will have PWN inside it.

```bash
echo PWN > COLLEGE
Correct! You successfully redirected 'PWN' to the file 'COLLEGE'! Here is your
flag:
pwn.college{kXjUAnCZxp95LR-L4RlqV0T77_C.QX0YTN0wyN5AzNzEzW}
```

### New Learnings
By default any output produced by commands like echo are in a destination called stdout which is the terminal screen, the > character is used to redirect such output to a specified location, if the file doesn't exist it gets created and if it does exist all its content gets overwritten.

### References 
-









## Challenge Name: Redirecting more output
This challenge is the same as the last one, except it shows any command's output can be redirected not just echo. /challenge/run command's output has to be redirected into a file called myflag.

### Solve
**Flag:** `pwn.college{kRK6bWhvrzTUf98hEvW5-uhhZvk.QX1YTN0wyN5AzNzEzW}`

To redirect output from /challenge/run to myflag: /challenge/run > myflag, > is the redirect operator.

```bash
/challenge/run > myflag
cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{kRK6bWhvrzTUf98hEvW5-uhhZvk.QX1YTN0wyN5AzNzEzW}
```

### New Learnings
> words to redirect output of any command.

### References 
-









## Challenge Name: Appending output
The challenge requires to append (not overwrite) the /challenge/run command's output into /home/hacker/the-flag using the >> operator to retrieve the entire flag (one half in the file written directly and the other half displayed on stdout).

### Solve
**Flag:** `pwn.college{Qq7imspBj9iMNKmqqRDnnMfMuwj.QX3ATO0wyN5AzNzEzW}`

Since the requirement is to append to the end of the /home/hacker/the-flag file and not overwrite all its content, the >> operator does the job. The full command would be /challenge/run >> /home/hacker/the-flag to transfer the output of /challenge/run to /home/hacker/the-flag.

```bash
cat /home/hacker/the-flag
 |
\|/ This is the first half:
 v
pwn.college{Qq7imspBj9iMNKmqqRDnnMfMuwj.QX3ATO0wyN5AzNzEzW}
                              ^
     that is the second half /|\
                              |
```

### New Learnings
The > operator will rewrite any previously existing data in an existing file, the >> operator will append to the end of an existing file.

### References 
-









## Challenge Name: Redirecting errors
Both output and errors can be redirected by using FD numbers, the goal is to redirect /challenge/run command's output into myflag and then redirect myflag's error into instructions to retrieve the flag.

### Solve
**Flag:** `pwn.college{of-nUUBY37v2GExuwRoH9NBNz3d.QX3YTN0wyN5AzNzEzW}`

By default > implies 1>, transfering output is the same as the last challenge: /challenge/run > myflag. To redirect errors the FD number is 2, so myflag 2> instructions, putting it all together: /challenge/run > myflag 2> instructions

```bash
/challenge/run > myflag 2> instructions
cat instructions
[PASS] The file at the other end of my stderr looks okay!
[PASS] Success! You have satisfied all execution requirements.
cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{of-nUUBY37v2GExuwRoH9NBNz3d.QX3YTN0wyN5AzNzEzW}

```

### New Learnings
Redirecting process communications is connected to FD numbers; FD 1 to redirect output (implicit), FD 2 to redirect errors, and FD 0 for standard inputs.
### References 
-









## Challenge Name: Redirecting input
There are two parts to the challenge; one: create PWN file with the CONTENT challenge in it (output redirection) and two: run /challenge/run using PWN file's content as input (input redirection)

### Solve
**Flag:** `pwn.college{sSuJT8-wnvnWU7T0jYGodpU1Hc2.QXwcTN0wyN5AzNzEzW}`

To redirect output: COLLEGE > PWN (COLLEGE is in file PWN)
To use PWN's content as input for /challenge/run instead of waiting for input: /challenge/run < PWN

```bash
echo COLLEGE > PWN
/challenge/run < PWN
Reading from standard input...
Correct! You have redirected the PWN file into my standard input, and I read
the value 'COLLEGE' out of it!
Here is your flag:
pwn.college{sSuJT8-wnvnWU7T0jYGodpU1Hc2.QXwcTN0wyN5AzNzEzW}
```

### New Learnings
Both input and output can be redirected, a command's input can be taken from another file by using the input redirection operation.

### References 
-









## Challenge Name: Grepping stored results
The challenge is to redirect output from /challenge/run to /tmp/data.txt and then using grep (search) to find the flag.

### Solve
**Flag:** `pwn.college{whag1R58vngi1KemF2XGpDDB1Jc.QX4EDO0wyN5AzNzEzW}`

Same as the other challenges, redirecting output: /challenge/run > /tmp/data.txt
Every flag begins with "pwn.college" so using grep to search through the thousands of lines of text: grep "pwn.college" /tmp/data.txt gives the flag

```bash
/challenge/run > /tmp/data.txt
grep "pwn.college" /tmp/data.txt
pwn.college{whag1R58vngi1KemF2XGpDDB1Jc.QX4EDO0wyN5AzNzEzW}
```

### New Learnings
Reinforcing output redirection and grep usage

### References 
-









## Challenge Name: Grepping live output
The challenge requires the usage of | (pipe) to avoid the making of temporary files and directly sending the output of /challenge/run to the grep function as input.

### Solve
**Flag:** `pwn.college{4NjUc-kEYuDzt8Zwtmvv8l_ryE7.QX5EDO0wyN5AzNzEzW}`

On the left of | is the stdout being taken and on the right of | is the standard input being given to the command which comes from the output of the command on the left. Essentially output of command 1 | input for command 2. The goal is to pass /challenge/run command's content into grep to search for the flag by avoiding the usage of making a temporary file like in the last challenge. So on the left is the stdout that will be the input for the grep command: /challenge/run and on the right is the command that needs to be run that will take /challenge/run command's output as input, since we need to grep to search for the flag, the right half is: grep "pwn.college". Putting it together: /challenge/run | grep "pwn.college"

```bash
/challenge/run | grep "pwn.college"
pwn.college{4NjUc-kEYuDzt8Zwtmvv8l_ryE7.QX5EDO0wyN5AzNzEzW}
```

### New Learnings
The | operator is an efficient way to connect two commands together, output of the command on the left is taken as input for the command on the right, this eliminates the need to redirect and make temporary files.

### References 
-









## Challenge Name
Add challenge description here

### Solve
**Flag:** `pwn.college{helloworld}`

type in your solve and your thought process behind solving the challenge. Include as much as info as possible. Use triple ticks for any bash commands and output you type on the terminal.

```bash
command 1
command 2
pwn.college{helloworld}
```

### New Learnings
Brief note on what you learned from the challenge

### References 
Add any references or videos you used while solving the challenge.









## Challenge Name
Add challenge description here

### Solve
**Flag:** `pwn.college{helloworld}`

type in your solve and your thought process behind solving the challenge. Include as much as info as possible. Use triple ticks for any bash commands and output you type on the terminal.

```bash
command 1
command 2
pwn.college{helloworld}
```

### New Learnings
Brief note on what you learned from the challenge

### References 
Add any references or videos you used while solving the challenge.
