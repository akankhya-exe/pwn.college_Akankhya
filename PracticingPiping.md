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
