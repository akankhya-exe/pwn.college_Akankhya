# Module Name: Pondering PATH

## Challenge Name: The PATH Variabe
The goal is to prevent the /challenge/run command from deleting the flag by giving the rm command a fake path.

### Solve
**Flag:** `pwn.college{odoOgg0x0YjJoNweHfpTBaBpi0f.QX2cDM1wyN5AzNzEzW}`

The goal is to make /challenge/run be unable to use the rm command.
To do this, set the PATH to an empty string for this command execution.
PATH="" /challenge/run
Now when the program tries to run rm, it'll search an empty PATH and fail to find a command and prints the flag instead.

```bash
PATH="" /challenge/run
Trying to remove /flag...
/challenge/run: line 4: rm: No such file or directory
The flag is still there! I might as well give it to you!
pwn.college{odoOgg0x0YjJoNweHfpTBaBpi0f.QX2cDM1wyN5AzNzEzW}
```

### New Learnings
PATH is a list of directories that the shell searches to find commands, without a valid PATH the shell cannot execute any commands. Used the temporary variable syntax to set up an environment variable for a
single command. 
A program's execution can be affected by disrupting its environment like manipulating its PATH variable.

### References 
-









## Challenge Name: Setting PATH
The goal is to run a command named win with the /challenge/run program except it's in another directory which isn't in the default PATH. The PATH needs to be set to this directory so that /challenge/run can
find and execute the win command.

### Solve
**Flag:** `pwn.college{MDdIlULcHgGPHBT4BDIsdmSqpuX.QX1cjM1wyN5AzNzEzW}`

The solution is to set the PATH variable just for the execution of /challenge/run which fails because it can't find the win command. So, set the PATH of /challenge/run to that of a directory that contains win.
PATH=/challenge/more_commands/ /challenge/run
For this command, the search path is /challenge/more_commands which contains the win command so /challenge/run will look through it, find the win command and execute it.

```bash
PATH=/challenge/more_commands/ /challenge/run
Invoking 'win'....
Congratulations! You properly set the flag and 'win' has launched!
pwn.college{MDdIlULcHgGPHBT4BDIsdmSqpuX.QX1cjM1wyN5AzNzEzW}
```

### New Learnings
PATHs can be customized by adding new directories and a program can be made readable by its own name by changing its PATH by having the relevant directory in PATH.

### References 
-









## Challenge Name: Finding Commands
The goal is to find the full path of the win command using which. The flag needs to be read from the same directory that win is located in.

### Solve
**Flag:** `pwn.college{0gO_MKR9qDLqJqN0gUVn41KsJX8.01NzEzNxwyN5AzNzEzW}`

First use which win to find the full path of the win command.
The output is /challenge/paths/11277/win
Since flag is in the same directory as win, flag belongs to /challenge/paths/11277/
So its full path is /challenge/paths/11277/flag.

```bash
which win
/challenge/paths/11277/win
cat /challenge/paths/11277/flag
pwn.college{0gO_MKR9qDLqJqN0gUVn41KsJX8.01NzEzNxwyN5AzNzEzW}
```

### New Learnings
which command searches directories in the PATH variable to find and display the full path of a given command.

### References 
-









## Challenge Name: Adding Commands
Add challenge description here

### Solve
**Flag:** `pwn.college{M9Jlu4zfTe2Yxs93UL5Z4TZp_aQ.QX2cjM1wyN5AzNzEzW}`

type in your solve and your thought process behind solving the challenge. Include as much as info as possible. Use triple ticks for any bash commands and output you type on the terminal.

```bash
which cat
/run/dojo/bin/cat
echo '#!/bin/bash' > ~/win
echo '/run/dojo/bin/cat /flag' >> ~/win
chmod +x ~/win
PATH=~/ /challenge/run
```

### New Learnings
Brief note on what you learned from the challenge

### References 
-










# Module Name

## Challenge Name
Add challenge description here

### Solve
**Flag:** `pwn.college{sOJT5p5tsSy-8TJea_vfG4bozar.QX3cjM1wyN5AzNzEzW}`

type in your solve and your thought process behind solving the challenge. Include as much as info as possible. Use triple ticks for any bash commands and output you type on the terminal.

```bash
which cat
/run/dojo/bin/cat
echo '#!/bin/bash' > ~/rm
echo '/run/dojo/bin/cat /flag' >> ~/rm
chmod +x ~/rm
PATH=~/ /challenge/run
Trying to remove /flag...
pwn.college{sOJT5p5tsSy-8TJea_vfG4bozar.QX3cjM1wyN5AzNzEzW}
```

### New Learnings
Brief note on what you learned from the challenge

### References 
-


