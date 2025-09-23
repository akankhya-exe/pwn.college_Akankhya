# Module Name: Digesting Documentation

## Challenge Name: Learning From Documentation
The challenge demonstrates a small usage of consulting documentation to find the necesssary arguments for a command

### Solve
**Flag:** `pwn.college{wTNERz-ZbwL5FHJs1tdJwmTio6w.QX0ITO0wyN5AzNzEzW}`

The goal is run the command /challenge/challenge with the correct arguments. The prompt gives a short piece of information about how to use the command (the documentation). The documenation clearly states the /challenge/challenge command needs to be used with the argument --giveflag. So, the entire command is /challenge/challenge --giveflag.

```bash
/challenge/challenge --giveflag
Correct argument! Here is your flag:
pwn.college{wTNERz-ZbwL5FHJs1tdJwmTio6w.QX0ITO0wyN5AzNzEzW}
```

### New Learnings
Documentation is an important part of understanding how any program works, documentation provides instructions and formats for using particular commands

### References 
-









## Challenge Name: Learning Complex Usage
The challenge requires to use the /challenge/challenge to print the flag. /challenge/challenge uses the --printfile argument which requires the correct flag file path.

### Solve
**Flag:** `pwn.college{0WcJ9mi6wzozEej_zW8aI1YyU5c.QX1ITO0wyN5AzNzEzW}`

According to the documentation, files can be printed using --printfile. It also says that --printfile itself requires an argument; the path of the file to be printed. The flag is inside /flag so the entire command according to the documentation would be /challenge/challenge --printfile /flag.

```bash
/challenge/challenge --printfile /flag
Correct argument! Here is the /flag file:
pwn.college{0WcJ9mi6wzozEej_zW8aI1YyU5c.QX1ITO0wyN5AzNzEzW}
```

### New Learnings
Arguments can also take arguments (like with find -name)
Documentation reading

### References 
-









## Challenge Name: Reading Manuals
The challenge requires reading the manual of the challenge command to find the secret command-line option to get the flag/

### Solve
**Flag:** `pwn.college{U2GvXCmpX2yZxdPQgBL_9xlscSN.QX0EDO0wyN5AzNzEzW}`

man challenge shows the manual for the challenge command, the NAME section gives the basic syntax of using the command, in the DESCRIPTION section all the arguments that can be used with the command are given.

--vmpyxd NUM
              print the flag if NUM is 229
sticks out
Combining the command from its argument in the documentation: /challenge/challenge --vmpyxd 229 is the secret command

```bash
man challenge
CHALLENGE(1)                                      Challenge Commands                                     CHALLENGE(1)

NAME
       /challenge/challenge - print the flag!

SYNOPSIS
       challenge OPTION

DESCRIPTION
       Output the flag when called with the right arguments.

       --fortune
              read a fortune

       --version
              output version information and exit

       --vmpyxd NUM
              print the flag if NUM is 229

AUTHOR
       Written by Zardus.

REPORTING BUGS
       The repository for this dojo: <https://github.com/pwncollege/linux-luminarium/>

SEE ALSO
       man(1) bash-builtins(7)
 Manual page challenge(1) line 1 (press h for help or q to quit)
 
/challenge/challenge  --vmpyxd 229
Correct usage! Your flag: pwn.college{U2GvXCmpX2yZxdPQgBL_9xlscSN.QX0EDO0wyN5AzNzEzW}
```

### New Learnings
The man command is used to pull up the manual (built-in documentation) for commands
The man page contains all its useful information in NAME, DESCRIPTION, and SYNOPSIS

### References 
-









## Challenge Name: Searching Manuals
The goal is to find the argument that completes the challenge command to give the flag by using the manual and the search function (/) to look for the needed argument

### Solve
**Flag:** `pwn.college{cfn4UPbvCL3UJF4bQXZhwbivij2.QX1EDO0wyN5AzNzEzW}`

man challenge brings up the manual for the command, / acts as a search function to look for specific commands and command descriptions, the most obvious search clue is 'flag' so by using /flag, it can be seen that --deyq argument has the description "This gives you the flag!".
Hence the required command is /challenge/challenge --deyq

```bash
man challenge
/challenge/challenge --deyq
Initializing...
Correct usage! Your flag: pwn.college{cfn4UPbvCL3UJF4bQXZhwbivij2.QX1EDO0wyN5AzNzEzW}
```

### New Learnings
/ is used to search in man pages (forward) and so is ? (backward)
n for next search result and N for previous search result

### References 
-









## Challenge Name: Searching For Manuals
The task is to find the argument for the /challenge/challenge program that will give the flag, except the manual for this has a randomized name. Hence the entire man database needs to be searched first, and then use the correct commands and searches to get to the required argument.

### Solve
**Flag:** `pwn.college{INca1GS3FNxl8-L9sol8DXABZHC.QX2EDO0wyN5AzNzEzW}`

First step is pulling the manual for the man command itself so man man. By using the search function for keywords like "search" (/), the -k option matches which searches descriptions of all available manuals
Now the man database can be used to search for any manual related to the word "challenge"; man -k challenge. On searching through the arguments --caxlso NUM (138) sticks out. On using /challenge/challenge --caxlso 138 the flag is printed.

```bash
man man
/search
man -k challenge
caxlsolwyz (1)       - print the flag!
/challenge/challenge  --caxlso 138
Correct usage! Your flag: pwn.college{INca1GS3FNxl8-L9sol8DXABZHC.QX2EDO0wyN5AzNzEzW}

```

### New Learnings
Manual about man itself is accessed using man man (meta-data)
man -k <keyword> allows searching of descriptions and looking for commands whose names you don't know

### References 
-









## Challenge Name: Helpful Programs
Not all programs are available on the man page but their descriptions can be invoked using special arguments usually --help, the challenge requires to find the arguments needed for the /challenge/challenge program by using the --help argument and going through its documentation

### Solve
**Flag:** `pwn.college{QgT41ifmGaDcqTZEeM9WIX83NnA.QX3IDO0wyN5AzNzEzW}`

The obvious starting point is to do /challenge/challenge --help as it's the program that needs to be run. On observing the documentation, -g gives the flag but requires another argument which relates to argument -p which gives the required argument for -g. Running /challenge/challenge -p gives the required last argument for -g. Combining everything: /challenge/challenge -g 419 gives the flag.

```bash
/challenge/challenge --help
usage: a challenge to make you ask for help [-h] [--fortune] [-v] [-g GIVE_THE_FLAG] [-p]

optional arguments:
  -h, --help            show this help message and exit
  --fortune             read your fortune
  -v, --version         get the version number
  -g GIVE_THE_FLAG, --give-the-flag GIVE_THE_FLAG
                        get the flag, if given the correct value
  -p, --print-value     print the value that will cause the -g option to give you the flag

/challenge/challenge -p
The secret value is: 419
/challenge/challenge -g 419
Correct usage! Your flag: pwn.college{QgT41ifmGaDcqTZEeM9WIX83NnA.QX3IDO0wyN5AzNzEzW}
```

### New Learnings
Not all commands are in the man database, but their own descriptions and synopsis can be invoked by special commands usually like --help (or -h)

### References 
-









## Challenge Name: Help for Builtins
Usage of builtins where challenge is a built in now not a program like /challenge/challenge, introduces the usage of help <builtin> to find the required arguments to access the flag

### Solve
**Flag:** `pwn.college{w29rE3EdD0pL8ZE0UnZmA9J4y8P.QX0ETO0wyN5AzNzEzW}`

It's explicitly stated that challenge is a builtin so --help doesn't work, and it's not a standard utility so man doesn't work, help challenge works here for builtins, the output provides the necessary information to complete the command and retrieve the flag, help challenge -secret w29rE3Ed.
```bash
help challenge
challenge: challenge [--fortune] [--version] [--secret SECRET]
    This builtin command will read you the flag, given the right arguments!

    Options:
      --fortune         display a fortune
      --version         display the version
      --secret VALUE    prints the flag, if VALUE is correct

    You must be sure to provide the right value to --secret. That value
    is "w29rE3Ed"
challenge --secret w29rE3Ed
Correct! Here is your flag!
pwn.college{w29rE3EdD0pL8ZE0UnZmA9J4y8P.QX0ETO0wyN5AzNzEzW}
```

### New Learnings
Commands like cd and exit aren't separate programs on the disk but are features directly built into the shell. These commands are necessary to modify the shell's own state.
help <builtin> is the command to find out more about a builtin.

### References 
-




