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
The goal is to execute the /challenge/run command whose sole purpose is to run the win command except the win command does not exist. win must be created in a script then modify the path so that /challenge/run
runs the win command defined in this script.

### Solve
**Flag:** `pwn.college{M9Jlu4zfTe2Yxs93UL5Z4TZp_aQ.QX2cjM1wyN5AzNzEzW}`

The script's job is to print the flag (/challenge/run should give the flag), use the full path to make sure it works with a modified PATH too while cat-ing.
echo '#!/bin/bash' > ~/win
echo '/bin/cat /flag' >> ~/win
This puts the flag in the win script.
Next make it executable with chmod +x 
The last step is to run the /challenge/run program but it's PATH must be specified to the home directory where the win script is so that /challenge/run will be forced to run the win script.
```bash
which cat
/run/dojo/bin/cat
echo '#!/bin/bash' > ~/win
echo '/run/dojo/bin/cat /flag' >> ~/win
chmod +x ~/win
PATH=~/ /challenge/run
```

### New Learnings
Custom commands can be created by making an executable script and putting its directory in the PATH variable to use while executing.

### References 
-










## Challenge Name: Hijacking Commands
The goal is to prevent /challenge/run from running the rm command and removing the flag by hijacking the rm command and making it print the flag instead.

### Solve
**Flag:** `pwn.college{sOJT5p5tsSy-8TJea_vfG4bozar.QX3cjM1wyN5AzNzEzW}`

The solution is to trick the /challenge/run program by creating a custom rm command and hijacking the PATH variable. First, a fake rm script is created in the home directory using echo '#!/bin/bash' > ~/rm followed by echo '/run/dojo/bin/cat /flag' >> ~/rm. This script is designed to ignore any arguments and simply print the contents of /flag using its full path. After being made executable with chmod +x ~/rm, the challenge is run with the command PATH=~/ /challenge/run. This forces the shell to search only the home directory, causing it to find and execute the fake rm script, which then prints the flag.

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
A command can be replaced with a custom defined command and can be made to run by manipulating the PATH variable, a command's functionality can be changed essentially.

### References 
-


