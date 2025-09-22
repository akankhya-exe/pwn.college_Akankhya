# Module Name: Pondering Paths

## Challenge Name: The Root
The challenge requires the user to invoke a program using its exact path, starting from / (absolute path)

### Solve
**Flag:** `pwn.college{QfAU8UBnSbu8g89jKGEAwu61qPD.QX4cTO0wyN5AzNzEzW}`

A program named pwn has been placed directly inside the root directory. / isn't a directory the shell normally searches for commands, so the absolute path must be provided.
Since pwn is directly inside / just running /pwn invokes the program.

```bash
/pwn
BOOM!!!
Here is your flag:
pwn.college{QfAU8UBnSbu8g89jKGEAwu61qPD.QX4cTO0wyN5AzNzEzW}
```

### New Learnings
All files and folders are in a single tree like structure, the absolute base beginning of the whole structure is the root directory which is represented by '/'. The absolute path is the full address that starts from the root directory / which is a good way to locate a file no matter what directory you're currently working in. Also, the shell must be told where to find a program by providing its path.

### References 
-









## Challenge Name: Program and absolute paths
The aim is to access a slightly more complicated path, running a program named run inside the /challenge/ directory. The absolute path must be used

### Solve
**Flag:** `pwn.college{wyuVKawSp04vpwqn3aEWODrNwBn.QX1QTN0wyN5AzNzEzW}`

The program is named run, which is inside the challenge directory, which itself is inside the root directory. The absolute path always begins with the root so /, and the first directory under this is challenge so /challenge, and lastly run is inside the challenge directory so /challenge/run is the full path.

```bash
/challenge/run
Correct!!!
/challenge/run is an absolute path! Here is your flag:
pwn.college{wyuVKawSp04vpwqn3aEWODrNwBn.QX1QTN0wyN5AzNzEzW}
```

### New Learnings
Reinforcement of absolute paths, writing paths for nested directories and accessing files that aren't inside the root directory and must be accessed using its structure hierarchy

### References 
-









## Challenge Name: Position thy self
Introduces the concept of navigating the filesystem using 'cd' (change directory), the original /challenge/run path isn't valid anymore and is inside a different hierarchy of directories that must be navigated to

### Solve
**Flag:** `pwn.college{4Qc3x-omf7gYVQkP0iDZYwOu2fz.QX2QTN0wyN5AzNzEzW}`

The problem says to first invoke /challenge/run which is obviously incorrect but the output gives the correct directory. On using cd /var/lib/apt/lists (previous command's output) it navigates to the correct directory where /challenge/run is inside. So the complete path is /var/lib/apt/lists/challenge/run.

```bash
~$ /challenge/run
Incorrect...
You are not currently in the /var/lib/apt/lists directory.
Please use the `cd` utility to change directory appropriately.
~$ cd /var/lib/apt/lists
/var/lib/apt/lists$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{4Qc3x-omf7gYVQkP0iDZYwOu2fz.QX2QTN0wyN5AzNzEzW}
```

### New Learnings
Shell prompt with the ~ or path shows where the user currently is and commands are executed from this location, learned to use cd to naviagate through the file structure as some programs require the user to be in a certain location

### References 
-









## Challenge Name: Position elsewhere
Another example of navigating using cd

### Solve
**Flag:** `pwn.college{Y_fIG0m9HfdNzwNvDh0fIO5sl7_.QX3QTN0wyN5AzNzEzW}`

The process is the same as the last challenge, just with a different lcoation to show variety in locations

```bash
~$ /challenge/run
Incorrect...
You are not currently in the /sys/kernel directory.
Please use the `cd` utility to change directory appropriately.
~$ cd /sys/kernel
/sys/kernel$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{Y_fIG0m9HfdNzwNvDh0fIO5sl7_.QX3QTN0wyN5AzNzEzW}
```

### New Learnings
Same as the last challenge, using cd to navigate through different directories

### References 
-









## Challenge Name: Position yet elsewhere
Same as the last two

### Solve
**Flag:** `pwn.college{A6G0D1hz3-LEu0VV-6sJwQKB0VK.QX4QTN0wyN5AzNzEzW}`

Used cd to navigate to the directory prompted my /challenge/run and ran /challenge/run in that directory

```bash
~$ /challenge/run
Incorrect...
You are not currently in the /sys/kernel directory.
Please use the `cd` utility to change directory appropriately.
~$ cd /sys/kernel
/sys/kernel$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{A6G0D1hz3-LEu0VV-6sJwQKB0VK.QX4QTN0wyN5AzNzEzW}
```

### New Learnings
Using to navigate between directories

### References 
-










## Challenge Name: implicit relative paths, from /
The challenge introduces relative paths which works relative to your current working directory, the goal is to run the absolute path /challenge/run using a relative path while in the root / directory

### Solve
**Flag:** `pwn.college{01COffQB4xUI13I57muctD5R1PY.QX5QTN0wyN5AzNzEzW}`

The starting location is /, since the absolute path is /challenge/run which is directly inside the cwd (and since relative paths don't start with a /), the relative path is simply challenge/run from the cwd.
Essentially, absolute path - current path/cwd

```bash
~$ cd /
/$ challenge/run
Correct!!!
challenge/run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{01COffQB4xUI13I57muctD5R1PY.QX5QTN0wyN5AzNzEzW}
```

### New Learnings
Relative paths are a way to access a file or directory in relation to the current working directory rather than using the absolute path, meaning the relative path changes depending on where you are
/challenge/run is a full absolute path
challenge/run is the path relative to the / directory

### References 
-









## Challenge Name: explicit relative paths, from /
The goal is to run /challenge/run using a relative path that explicitly includes '.' to indicate the current working directory

### Solve
**Flag:** `pwn.college{Qh4ANd-U4IuGLvGpSVh6vRn0ivi.QXwUTN0wyN5AzNzEzW}`

Target location is /challenge/run, by using cd /, location is set to / directory, now challenge/run is inside this / directory which makes it the current directory, and '.' is used to indicate to search inside the current directory so ./challenge/run invokes the program after searchin for it in the current directory

```bash
~$ cd /
/$ ./challenge/run
Correct!!!
./challenge/run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{Qh4ANd-U4IuGLvGpSVh6vRn0ivi.QXwUTN0wyN5AzNzEzW}
```

### New Learnings
Using the ./ prefix, ./location_name is the standard way to run a file in the current directory, it's an explicit notation that tells the shell to find the program right in the current directory and solves ambiguity.

### References 
-









## Challenge Name: implicit relative path
The challenge requires to execute the run program while being inside the challenge directory and use the correct relative path syntax

### Solve
**Flag:** `pwn.college{cyHAagax6Bt64miIQx1o8dKrxJP.QXxUTN0wyN5AzNzEzW}`

The challenge specifies being in the challenge directory so the command is cd /challenge, now the run program is inside the challenge directory as stated in the challenge, since run is in the correct directory the ./ prefix must be used, so the entire command is ./run which searches for run in the challenge directory and executes it

```bash
~$ cd /challenge
/challenge$ ./run
Correct!!!
./run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{cyHAagax6Bt64miIQx1o8dKrxJP.QXxUTN0wyN5AzNzEzW}
```

### New Learnings
Shell intentionally does not search the current directory for commands by default as a security feature, to run a program within the current directory explicit command has to be given with the ./ prefix to signal to the Shell that I want to run a program intentionally.

### References 
-









## Challenge Name: home sweet home
Make the /challenge/run program save the flag into a file. The program must be provided with an argument for the output file which must be an absolute path, inside the home directory, and no more than three characters before expanding.

### Solve
**Flag:** `pwn.college{QjfCXzz7gDHH5RkxeZ9DP_uODhz.QXzMDO0wyN5AzNzEzW}`

The goal is to provide a path that is only three characters long but is valid when expanded, the ~ operator is the apt choice as it expands into the home directory and it's only one character, so the shortest way to specify the path in the home directory (~) would be ~/a which creates a file named 'a' and writes the flag into it

```bash
~$ /challenge/run ~/a
Writing the file to /home/hacker/a!
... and reading it back to you:
pwn.college{QjfCXzz7gDHH5RkxeZ9DP_uODhz.QXzMDO0wyN5AzNzEzW}
```

### New Learnings
~ is a shortcut that the shell expands into the full home directory path, passing arguments to programs (~/a) which told the /challenge/run program to perform a writing into file task

### References 
-





