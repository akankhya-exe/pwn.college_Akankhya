# Module Name: Chaining Commands

## Challenge Name: Chaining with Semicolons
To get the flag, chain /challenge/pwn and /challenge/college together.

### Solve
**Flag:** `pwn.college{helloworld}`

To chain two commands together, seperate them using a semicolon: <command1> ; <command2>

```bash
/challenge/pwn; /challenge/college
Yes! You chained /challenge/pwn and /challenge/college! Here is your flag:
pwn.college{A_ErssMi_Uow9KQ0UflbOeN6QCh.QX1UDO0wyN5AzNzEzW}
```

### New Learnings
Semicolons can be used to chain commands together.

### References 
-









## Challenge Name: Building on Success
The goal is to chain together /challenge/first-success and /challenge/second, but the 2nd only runs if the first one runs successfully

### Solve
**Flag:** `pwn.college{helloworld}`

To use "AND" logic (command 2 runs if and only if command 1 is successful), the && operator is used: /challenge/first-success && /challenge/second means /challenge/second will run if /challenge/first-success is
successfully executed

```bash
/challenge/first-success && /challenge/second
Nice chaining! Flag: pwn.college{85svNj20LEJKdhV_Xpdn660pCmQ.0lM0MDOxwyN5AzNzEzW}
```

### New Learnings
&& is used to execute AND logic (both must be true)

### References 
-









## Challenge Name: Handling Failure
The goal is to run /challenge/first-failure and /challenge/second by chaining them together, except the first command fails so || has to be used.

### Solve
**Flag:** `pwn.college{4qIQG3UU8xyFhdjnxkDWCUKCj2O.01M0MDOxwyN5AzNzEzW}}`

|| uses "OR" logic meaning if command 1 fails, only then does command 2 run, so since the question says /challenge/first-failure WILL fail to run, /challenge/second will run instead as its the second command in the chain
and the first one failed.
So: /challenge/first-failure || /challenge/second

```bash
/challenge/first-failure || /challenge/second
Nice chaining! Flag: pwn.college{4qIQG3UU8xyFhdjnxkDWCUKCj2O.01M0MDOxwyN5AzNzEzW}
```

### New Learnings
|| is used to implement "OR" logic, the second command runs if the first one fails, otherwise only the first one runs.

### References 
-









## Challenge Name: Your First Shell Script
The goal is create a shell script named x.sh and in it are two commands: /challenge/pwn and /challenge/college.

### Solve
**Flag:** `pwn.college{M2iHgEa7nyWkfFFt2Rwvq85NE7o.QXxcDO0wyN5AzNzEzW}`

First create a shell script called x.sh and redirect /challenge/pwn using the > operator. The same applies for the /challenge/college command too except >> operator to be used to append otherwise the first
one will be overwritten. To run the shell script use bash x.sh bash creates new instance of the shell.

```bash
echo "/challenge/pwn" > x.sh
echo "/challenge/college" >> x.sh
bash x.sh
Great job, you've written your first shell script! Here is the flag:
pwn.college{M2iHgEa7nyWkfFFt2Rwvq85NE7o.QXxcDO0wyN5AzNzEzW}
```

### New Learnings
A shell script is a text file containing a list of shell commands executed in order. Scripts allow re-running of complex or repetitive tasks by keeping the sequence in one place.
bash <shell script> tells the script to read the command from the file instead of from the terminal

### References 
-









## Challenge Name: Redirecting Script Output
The goal is to pipe multiple commands at once, /challenge/pwn and /challenge/college have to be piped into /challenge/solved.

### Solve
**Flag:** `pwn.college{helloworld}`

A shell script is essentially a collection of executable commands, to pipe multiple commands at once, the first step is to put them all in a script shell file. So echo "/challenge/pwn" > x.sh and same for the
other command too. Now both commands are in the script x.sh. This can be treated as a singular command and piped into /challenge/solve. So bash x.sh | /challenge/solve.

```bash
echo "/challenge/pwn" > x.sh
echo "/challenge/college" >> x.sh
bash x.sh | /challenge/solve
Correct! Here is your flag:
pwn.college{0IUb5jQVQz3hIrTbQcOZIAGWaov.QX4ETO0wyN5AzNzEzW}
```

### New Learnings
Multiple commands can be piped using shell scripts.

### References 
-









## Challenge Name: Executable Shell Scripts
The goal is to create a shell script x.sh and run it without using bash in front of it. This is achieved by giving execution perms.

### Solve
**Flag:** `pwn.college{8RBtsRJrHiyQzLO1JeirSjBag7-.QX0cjM1wyN5AzNzEzW}`

The command /challenge/solve needs to be stored in a shell script according to the question so echo "/challenge/solve" > x.sh. Now bash is used to specify exeuction of the script shell, but this can be avoided
if direct perms are given to access the file, chmod +x can be used to give execution access for the shell script and then it can be run as a normal command/file without having to specify bash.
So chmod +x x.sh gives the required execution permissions.

```bash
echo "/challenge/solve" > x.sh
chmod +x x.sh
./x.sh
Congratulations on your shell script execution! Your flag:
pwn.college{8RBtsRJrHiyQzLO1JeirSjBag7-.QX0cjM1wyN5AzNzEzW}
```

### New Learnings
A script can be executed directly by making it executable using perms and running it as normal instead of having to prefix it with bash every time.

### References 
-









## Challenge Name: Understanding Shebangs
Add challenge description here

### Solve
**Flag:** `pwn.college{UNjHGHhDP5LpOwbcIcoDnAPr4MO.0VOzMDOxwyN5AzNzEzW}`

type in your solve and your thought process behind solving the challenge. Include as much as info as possible. Use triple ticks for any bash commands and output you type on the terminal.

```bash
echo '#!/bin/bash' > /home/hacker/solve.sh
echo 'echo "hack the planet"' >> /home/hacker/solve.sh
chmod +x /home/hacker/solve.sh
/challenge/run
Testing your script...
Perfect! Your flag:
Flag: pwn.college{UNjHGHhDP5LpOwbcIcoDnAPr4MO.0VOzMDOxwyN5AzNzEzW}
```

### New Learnings
Brief note on what you learned from the challenge

### References 
Add any references or videos you used while solving the challenge.








