# Module Name: Shell Variables

## Challenge Name: Printing Variables
This challenge introduces the concept of variables and how to print them, the variable FLAG has to be printed to get the flag.

### Solve
**Flag:** `pwn.college{04mo5DbCrqAxWV4rxKqYnJKkqYV.QX3UTN0wyN5AzNzEzW}`

Variables are printed by prepending them with $ and echo is used to print so echo $FLAG

```bash
echo $FLAG
pwn.college{04mo5DbCrqAxWV4rxKqYnJKkqYV.QX3UTN0wyN5AzNzEzW}
```

### New Learnings
Variables can be printed by prepending them with $

### References 
-









## Challenge Name: Setting Variables
This challenge introduces setting variables, the goal is to set the variable PWN to COLLEGE in order to get the flag.

### Solve
**Flag:** `pwn.college{8oNQQx4Lgwz8itZwAwGQbagsIbg.QX5UTN0wyN5AzNzEzW}`

To assign a variable it does not need to be prepended with $ (only when accessing it), so the command is simply variable=value; PWN=COLLEGE

```bash
PWN=COLLEGE
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{8oNQQx4Lgwz8itZwAwGQbagsIbg.QX5UTN0wyN5AzNzEzW}
```

### New Learnings
Variables can be assigned using the = operator.

### References 
-









## Challenge Name: Multi-word Variables
The goal is to assign variable PWN with the value COLLEGE YEAH while handling multi-word arguments using ""
### Solve
**Flag:** `pwn.college{453gS8o3KYEZdfKxU1B1ygDqRoG.QXwYTN0wyN5AzNzEzW}`

When there's a space between the values of the data being assigned to the variable it is interpreted as the next command, to use multi-word variables "" needs to be used around the data.

```bash
PWN="COLLEGE YEAH"
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{453gS8o3KYEZdfKxU1B1ygDqRoG.QXwYTN0wyN5AzNzEzW}
```

### New Learnings
Multi-word variables can be initialized using "".

### References 
Add any references or videos you used while solving the challenge.









## Challenge Name: Exporting Variables
The challenge is to run /challenge/run with PWN which is an exported value whose value is the string COLLEGE (child process sees this) but COLLEGE holds the value PWN and is not exported so /challenge/run (can't inherit COLLEGE variable).

### Solve
**Flag:** `pwn.college{gQUHdsY0notlX4qmmFF_R_zQFBh.QXyYTN0wyN5AzNzEzW}`

Exported variables can be seen by other processes, since PWN=COLLEGE is an exported variable, /challenge/run can use it, on the other hand the non-exported COLLEGE variable would not work with /challenge/run since it does not exist in the environment.

```bash
export PWN=COLLEGE
You've set the PWN variable to the proper value!
COLLEGE=PWN
You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!
/challenge/run PWN
CORRECT!
You have exported PWN=COLLEGE and set, but not exported, COLLEGE=PWN. Great
job! Here is your flag:
pwn.college{gQUHdsY0notlX4qmmFF_R_zQFBh.QXyYTN0wyN5AzNzEzW}
```

### New Learnings
Unexported variables are like local variables that can't be used by outside commands or programs, on exporting variables they become "global" and can be used by other commands.

### References 
-









## Challenge Name: Printing exported variables
The goal is to access all the exported variables using the env command to find the FLAG variable and its value which is an exported variable.

### Solve
**Flag:** `pwn.college{MDLnO73zA6r9Hqb1u4LacXersb9.QX4UTN0wyN5AzNzEzW}`

The challenge is to access exported variables, specifically through the env command which shows all exported variables along with their values. So simply typing 'env' gives a list of all exported variables where the FLAG variable can be found.

```bash
env
SHELL=/run/dojo/bin/bash
HOSTNAME=variables~printing-exported-variables
PWD=/home/hacker
MANPATH=/run/dojo/share/man:
DOJO_AUTH_TOKEN=2ce3afc192f7790a448a7d500fd5f99e47ca27edb5b4b036a7e6d7a5d3eedf50
HOME=/home/hacker
LANG=C.UTF-8
FLAG=pwn.college{MDLnO73zA6r9Hqb1u4LacXersb9.QX4UTN0wyN5AzNzEzW}
```

### New Learnings
env command can be used to see all exported variables.

### References
-









## Challenge Name: Storing Command Output
The challenge is to store the output /challenge/run in a variable PWN and read it to get the flag.

### Solve
**Flag:** `pwn.college{cWqRXqwI0GqQZXMS-hK0uOTeizO.QX1cDN1wyN5AzNzEzW}`

A variable can hold the output of a command also if it is prepended by the $ symbol, therefore $(/challenge/run) gives the output which is then assigned to the variable PWN.

```bash
PWN=$(/challenge/run)
echo $PWN
pwn.college{cWqRXqwI0GqQZXMS-hK0uOTeizO.QX1cDN1wyN5AzNzEzW}
```

### New Learnings
Variables can be assigned the outputs of commands also by using $.

### References 
-









## Challenge Name: Reading Input
The challenge is to read the value "COLLEGE" into the variable PWN by inputting using the read command.

### Solve
**Flag:** `pwn.college{YgBSJRHFzSThGVFE8wLgIzdYDaM.QX4cTN0wyN5AzNzEzW}`

To read into a variable the syntax is read <variable name> and then the shell waits until user input is entered and assigns the input to the variable.

```bash
read PWN
COLLEGE
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{YgBSJRHFzSThGVFE8wLgIzdYDaM.QX4cTN0wyN5AzNzEzW}
```

### New Learnings
read command is used to take user input

### References 
-









## Challenge Name: Reading Files
The challenge is to use the read command to read the /challenge/read_me into the PWN environment variable.

### Solve
**Flag:** `pwn.college{QOg7iC3-0_Dmc3xcQ2YQaHFElyl.QXwIDO0wyN5AzNzEzW}`

($cat file) works but it wastes a call, so the shell's builtin read can take data directly from a file if path is given using the < operator to store it in the PWN variable.

```bash
read PWN < /challenge/read_me
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{QOg7iC3-0_Dmc3xcQ2YQaHFElyl.QXwIDO0wyN5AzNzEzW}
```

### New Learnings
A file's output can directly be fed into a variable.

### References 
-
