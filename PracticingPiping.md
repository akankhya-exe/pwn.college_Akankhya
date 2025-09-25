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









## Challenge Name: Grepping errors
The challenge requires to redirect the standard error of /challenge/run into the grep command using pipeline, except | by definition only takes standard output streams, so the goal is to redirect using the >& operator to redirect the output and workaround the | limitation.

### Solve
**Flag:** `pwn.college{g-oaWCFpmhdNoTEwclEHzke-jin.QX1ATO0wyN5AzNzEzW}`

By defitnition the | operator redirects standard output of the left half into the process of the right and has no effect on FD 2. This can be solved by using >& operator to merge streams; by using 2>&1 it instructs the shell to point to the same direction that FD 1 (stdout) is currently pointed to, this essentially merges the two.
/challenge/run on using 2>&1 makes the stderr of /challenge/run point to its stdout instead. So now output and error are both at the stdout stream. Then regular usage of grep to find the flag.

```bash
/challenge/run 2>&1 | grep "pwn.college"
pwn.college{g-oaWCFpmhdNoTEwclEHzke-jin.QX1ATO0wyN5AzNzEzW}
```

### New Learnings
>& can be used to redirect a file descriptor into another file descriptor, in this case error (not handled by |) can be redirected into output so that it can be fed as "stdout" into the | command.

### References 
-









## Challenge Name: Filtering with grep -v
The goal is to extract from the /challenge/run file that has loads of decoy files using the grep -v (inverted grep) command to exclude the decoy files.

### Solve
**Flag:** `pwn.college{YCYtaF6br0Xg8kZVrDfrfT0XH7w.0FOxEzNxwyN5AzNzEzW}`

The argument given to grep -v is excluded from all searches, so any file with the word "DECOY" in it should be excluded, therefore the command is grep -v DECOY.

```bash
/challenge/run | grep -v DECOY
pwn.college{YCYtaF6br0Xg8kZVrDfrfT0XH7w.0FOxEzNxwyN5AzNzEzW}
```

### New Learnings
grep -v can be used to exclude words from its searches.

### References 
-









## Challenge Name: Duplicating piped data with tee
The goal is to pipe /challenge/pwn into /challenge/college by using the tee command to intercept the /challenge/pwn program using tee to see what pwn needs to give the flag.

### Solve
**Flag:** `pwn.college{ceC7u2cltjJ-POzuN52fz2jU7tS.QXxITO0wyN5AzNzEzW}`

Just doing /challenge/pwn | /challenge/college gives an error which cannot be traced as stdout cannot be seen. Using tee to intercept the output of /challenge/pwn into another file called bug, and then using cat bug to see what /challenge/pwn needs. The bug file clearly states what extra arguments that /challenge/pwn needs in order to work, the last step is to pipe /challenge/pwn with the right --secret argument into /challenge/college.

```bash
/challenge/pwn | tee bug | /challenge/college

cat bug
Usage: /challenge/pwn --secret [SECRET_ARG]

SECRET_ARG should be "ceC7u2cl"

/challenge/pwn --secret ceC7u2cl | /challenge/college
Processing...
Correct! Passing secret value to /challenge/college...
Great job! Here is your flag:
pwn.college{ceC7u2cltjJ-POzuN52fz2jU7tS.QXxITO0wyN5AzNzEzW}
```

### New Learnings
tee command is used as a splitter to send the std input to two or more locations simulatenously: stdout and any files specified in the arguments

### References 
-









## Challenge Name: Process substitution for input
The goal is to use find the difference between the /challenge/print_decoys and /challenge/print_decoys_and_flag by using process substitution to treat the output of a command as a file instead of creating separate temporary files.

### Solve
**Flag:** `pwn.college{kScZkOFusT5YqANw5acqZkcPlAW.0lNwMDOxwyN5AzNzEzW}`

The diff command is used to compare two input files the syntax is: diff file1 file2. Now instead of creating two separate temporary files, process substituion will be used to directly use the output of /challenge/print_decoys and /challenge/print_decoys_and_flag so instead of writing file1 file2 the command is: diff <(/challenge/print_decoys) <(/challenge/print_decoys_and_flag)

```bash
diff <(/challenge/print_decoys) <(/challenge/print_decoys_and_flag)
75a76
> pwn.college{kScZkOFusT5YqANw5acqZkcPlAW.0lNwMDOxwyN5AzNzEzW}
```

### New Learnings
<(command) syntax of process substitution is used to treat the output of the command as a temporary file, useful for commands like cat and diff that take file names as arguments.

### References 
-









## Challenge Name: Writing to multiple programs
The challenge is to run one program /challenge/hack and sends its output as input to two other programs /challenge/the and /challenge/planet at the same time, combining the usage of |, tee and process substituton as | only allows connection of one program to another single program only, not more than one.

### Solve
**Flag:** `pwn.college{U96v1fRzsfpWl8psy-nA_Emzl7U.QXwgDN1wyN5AzNzEzW}`

The intitial problem is that | can connect only one command's output to the other command's input, output cannot be sent to two places using just |. However tee command is used to split an input stream into multiple output streams: stdout and other files. But, tee command is designed to write into other files but the goal is to write into another program, so process substitution >(command) can be used to make the program's input look like a file when it's actually just another program. Assembling everything: /challenge/hack | tee >(/challenge/the) >(/challenge/planet). The two arguments for tee are the destinations or the two "files" to be written into.

```bash
/challenge/hack | tee >(/challenge/the) >(/challenge/planet)
This secret data must directly and simultaneously make it to /challenge/the and
/challenge/planet. Don't try to copy-paste it; it changes too fast.
35294778291184620
Congratulations, you have duplicated data into the input of two programs! Here
is your flag:
pwn.college{U96v1fRzsfpWl8psy-nA_Emzl7U.QXwgDN1wyN5AzNzEzW}
```

### New Learnings
tee can be used to read data and duplicate it to multiple destinations (stdout and multiple files), tee can be combined with >(command) to overcome the need for tee to only write into normal files, tee can used to split input into other programs too by using >.

### References 
-







## Challenge Name: Split-piping stderr and stdout
The challenge is to execute a single program, /challenge/hack and pipe its standard output to /challenge/planet and simultaneously redirect its error to /challenge/the program at once.

### Solve
**Flag:** `pwn.college{4Aje_wpvSi-dfTL2kMLHSAUI1PW.QXxQDM2wyN5AzNzEzW}`

To do the stdout part: /challenge/hack | /challenge/planet is simply using |. This only handles stdout so the stderr would be left over and just print onto the terminal. To redirect stderr 2> is used except it takes a file as destination not another program so >(command) has to be used to use it as a temporary file, so redirecting stderr looks like: /challenge/hack 2> (>/challenge/the). Putting it all together gives: /challenge/hack 2> >(/challenge/the) | /challenge/planet
```bash
/challenge/hack 2> >(/challenge/the) | /challenge/planet
Congratulations, you have learned a redirection technique that even experts
struggle with! Here is your flag:
pwn.college{4Aje_wpvSi-dfTL2kMLHSAUI1PW.QXxQDM2wyN5AzNzEzW}
```

### New Learnings
stderr and stdout are completely different streams that can be routed independently to different destinations; | for stdout and 2> for stderr.
/challenge/hack 2> >(/challenge/the) | /challenge/planet ; in this command >(/challenge/the) is not an argument to the pipe, they are two separate instructions for /challenge/hack

### References 
https://askubuntu.com/questions/625224/how-to-redirect-stderr-to-a-file









## Challenge Name: Named pipes
The goal is to create a named pipe (FIFO) to get the flag from /challenge/run. First a pipe has to be created at /tmp/flag_fifo and then redirect the program's output into it. FIFOs block until a reader is present, it will only function is there's a writer and reader at the two ends.

### Solve
**Flag:** `pwn.college{4zKfaUHL59GNM73LrE7lfGXRdr-.01MzMDOxwyN5AzNzEzW}`

First create the FIFO using mkfifo /tmp/flag_fifo, the fifo has to be opened for reading (use cat) and then this will wait or block til another program opens the pipe, in another terminal the /challenge/run program's output can be redirected to the fifo.


```bash
mkfifo /tmp/flag_fifo
cat /tmp/flag_fifo

You've correctly redirected /challenge/run's stdout to a FIFO at
/tmp/flag_fifo! Here is your flag:
pwn.college{4zKfaUHL59GNM73LrE7lfGXRdr-.01MzMDOxwyN5AzNzEzW}
```
{In another terminal}

```bash
/challenge/run > /tmp/flag_fifo
You're successfully redirecting /challenge/run to a FIFO at /tmp/flag_fifo!
Bash will now try to open the FIFO for writing, to pass it as the stdout of
/challenge/run. Recall that operations on FIFOs will *block* until both the
read side and the write side is open, so /challenge/run will not actually be
launched until you start reading from the FIFO!
```

### New Learnings
FIFOs act like communication channels (kind of like walkie-talkies as an easier analogy) that act over processes without writing anything onto the disk. mkfifo is the command to make pipes. FIFO blocks (waits) until both the reading and writing ends are in use (synchronization). A named pipe allows any two files to interact as long as they use the same FIFO. | only connects commands on a single line.

### References 
https://www.geeksforgeeks.org/cpp/named-pipe-fifo-example-c-program/ (for understanding FIFOs)
