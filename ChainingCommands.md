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
The goal is to create an executable shell script, it must have a shebang on its first line (#!) to tell the system what interpreter to use. The script script.sh needs to have the phrase "hack the planet", be
made executable for the flag to be retrieved.

### Solve
**Flag:** `pwn.college{UNjHGHhDP5LpOwbcIcoDnAPr4MO.0VOzMDOxwyN5AzNzEzW}`

The shebang tells the OS which interpreter to run the script with, the standard bash interpreter is /bin/bash for the shebang is #!/bin/bash which needs to be the first line of the script, next add the required 'hack the planet' phrase in the same script using the > and >> operators. So echo '#!/bin/bash' > solve.sh and and echo 'echo "hack the planet"' >> solve.sh (two echos to be able to print).
To make it executable perms have be changed using chmod +x. The flag file can now be run.

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
The shebang is the first line of a shell script which tells the OS which interpreter to use, the script is now self-sufficient, the script knows how to run without having to explicitly type bash in the beginning.

### References 
-









## Challenge Name
The goal is to write a shell script named /home/hacker/solve.sh that takes two command arguments and then prints them in reverse.

### Solve
**Flag:** `pwn.college{4d3MPyFV_JR-anT3L3cRAKCrRdf.0VNzMDOxwyN5AzNzEzW}`

The script needs to firstly access the first and second arguments. Variables are stored in the form of $1 $2. To print them in reverse, $2 needs to be printed followed by $1. The echo command can be written
as echo "$2 $1"
/home/hacker/solve.sh is created with the relevant commands: #!/bin/bash for shebang and then to output in reverse put $2 first and $1 second. Change file perms and run.

```bash
echo '#!/bin/bash' > /home/hacker/solve.sh
echo 'echo "$2 $1"' >> /home/hacker/solve.sh
chmod +x /home/hacker/solve.sh
/challenge/run
Correct! Your script properly reversed the arguments.
Here's your flag:
pwn.college{4d3MPyFV_JR-anT3L3cRAKCrRdf.0VNzMDOxwyN5AzNzEzW}
```

### New Learnings
$1 and $2 are positional arguments, $1, $2 etc are used to access the arguments passed to it in order.

### References 
-









## Challenge Name: Scripting with Conditionals
The goal is to write a script that uses conditional logic. The /home/hacker/solve.sh script has to check if the argument is pwn and print college, otherwise print nothing.

### Solve
**Flag:** `pwn.college{klyA64OLs8YnDR7Yuph91nu0sLk.0lNzMDOxwyN5AzNzEzW}`

The logic constructed is:
if [ "$1" == "pwn" ]; then
  echo "college"
fi

then input this structure line by line into the /home/hacker/solve.sh script and give relevant execution permissions.

```bash
echo '#!/bin/bash' > /home/hacker/solve.sh
echo 'if [ "$1" == "pwn" ]; then' >> /home/hacker/solve.sh
echo '  echo "college"' >> /home/hacker/solve.sh
echo 'fi' >> /home/hacker/solve.sh
chmod +x /home/hacker/solve.sh
/challenge/run
Correct! Your script properly handles all the conditions.
Here's your flag:
pwn.college{klyA64OLs8YnDR7Yuph91nu0sLk.0lNzMDOxwyN5AzNzEzW}
```

### New Learnings
Conditional logic can be added to scripts for deicison making, different actions can be made based on different decisions.
[] contains the test condition.

### References 
-










## Challenge Name: Scripting with Default Cases
The goal is to write an if/else block that has two possible outcomes, the logic should be in the /home/hacker/solve.sh file, if the argument is "pwn" output should be "college" otherwise output should be "nope".

### Solve
**Flag:** `pwn.college{YA2aeKQRcnvFT3BQLJYBHT8Acw1.01NzMDOxwyN5AzNzEzW}`

The logic is:
if [ "$1" == "pwn" ]; then
  echo "college"
else
  echo "nope"
fi

Input every line into the script file and give execution perms.

```bash
echo '#!/bin/bash' > /home/hacker/solve.sh
echo 'if [ "$1" == "pwn" ]; then' >> /home/hacker/solve.sh
echo '  echo "college"' >> /home/hacker/solve.sh
echo 'else' >> /home/hacker/solve.sh
echo '  echo "nope"' >> /home/hacker/solve.sh
echo 'fi' >> /home/hacker/solve.sh
chmod +x /home/hacker/solve.sh
/challenge/run
Correct! Your script properly handles the if/else conditions.
Here's your flag:
pwn.college{YA2aeKQRcnvFT3BQLJYBHT8Acw1.01NzMDOxwyN5AzNzEzW}
```

### New Learnings
else block provides an outcome mechanism in case the if block is false, different decisions can be made.

### References 
-









## Challenge Name
Add challenge description here

### Solve
**Flag:** `pwn.college{EMiVECCtA1hEjq1khMzNIk0_27n.0FOzMDOxwyN5AzNzEzW}`

Logic:
if [ "$1" == "hack" ]; then
  echo "the planet"
elif [ "$1" == "pwn" ]; then
  echo "college"
elif [ "$1" == "learn" ]; then
  echo "linux"
else
  echo "unknown"
fi

```bash
echo '#!/bin/bash' > /home/hacker/solve.sh
echo 'if [ "$1" == "hack" ]; then' >> /home/hacker/solve.sh
echo '  echo "the planet"' >> /home/hacker/solve.sh
echo 'elif [ "$1" == "pwn" ]; then' >> /home/hacker/solve.sh
echo '  echo "college"' >> /home/hacker/solve.sh
echo 'elif [ "$1" == "learn" ]; then' >> /home/hacker/solve.sh
echo '  echo "linux"' >> /home/hacker/solve.sh
echo 'else' >> /home/hacker/solve.sh
echo '  echo "unknown"' >> /home/hacker/solve.sh
echo 'fi' >> /home/hacker/solve.sh
chmod +x /home/hacker/solve.sh
/challenge/run
```

### New Learnings
elif clause if used to implement multiple condition checks.

### References 
-










## Challenge Name: Reading Shell Scripts
The goal is to find the password inside the /challenge/run shell script, get the password and run the program with the provided password.

### Solve
**Flag:** `pwn.college{helloworld}`

First use cat to read the file, clearly according to the if statement the "guess" argument has to be hack the PLANET for the flag to work. Run /challenge/run with the password and get the flag.

```bash
cat /challenge/run
#!/opt/pwn.college/bash

read GUESS
if [ "$GUESS" == "hack the PLANET" ]
then
        echo "CORRECT! Your flag:"
        cat /flag
else
        echo "Read the /challenge/run file to figure out the correct password!"

/challenge/run
hack the PLANET
CORRECT! Your flag:
pwn.college{U61GAdsOM3U7mIrNjEWNx9pHc2b.0lMwgDOxwyN5AzNzEzW}
```

### New Learnings
Scripts can be open and read, simple tools can be used to read what the program is doing.

### References 
-






