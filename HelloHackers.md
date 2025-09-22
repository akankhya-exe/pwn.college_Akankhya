# Module Name: Hello Hackers

## Challenge Name: Intro to Commands
The challenge requires the user to invoke the 'hello' command and observe how when the command terminates, the shell prompt comes up again

### Solve
**Flag:** `pwn.college{A5LYd2W8kqj-vMVM34yAnqAOECW.QX3YjM1wyN5AzNzEzW}`

Typing the 'hello' command to invoke it which presents the flag, terminal prompts again once one command terminates

```bash
hello
pwn.college{A5LYd2W8kqj-vMVM34yAnqAOECW.QX3YjM1wyN5AzNzEzW}
```

### New Learnings
Command prompts and terminations, commands are case sensitive

### References 
-









## Challenge Name: Intro to Arguments
The challenge introduces 'arguments' given to commands, arguments can be thought of as extra information that tell a command what to do or what to act on, without arguments commands would be quite limited.

### Solve
**Flag:** `pwn.college{MlDIT4qEeNdAp9CJ-8ssBpRj0iq.QX4YjM1wyN5AzNzEzW}`

By using 'hello hackers' in the terminal, the echo command is invoked with the argument 'hello hackers', the echo command is used to display a string of text, the argument is the string of text to display

```bash
hello hackers
pwn.college{MlDIT4qEeNdAp9CJ-8ssBpRj0iq.QX4YjM1wyN5AzNzEzW}
```

### New Learnings
Structure of a command (the first word which is the program to be executed), and the subsequent pieces which are the arguments and tells the command what to do
The shell parses it and splits it into commands and arguments and then returns the expected output

### References 
-









## Challenge Name: Command History
This challenge introduces the concept of command history, the shell remembers every command and entered and these commands can be easily accessed.

### Solve
**Flag:** `pwn.college{UPwDVy8cNcKh3ID6X_cZA7PV7aQ.0lNzEzNxwyN5AzNzEzW}`

Used the arrow keys (up arrow in this case) to cycle through past commands and come across the injected flag in my command history

```bash
pwn.college{UPwDVy8cNcKh3ID6X_cZA7PV7aQ.0lNzEzNxwyN5AzNzEzW}
```

### New Learnings
Command history can be used to quickly access previous commands instead of having to retype them and risk making typos, this can be done using the up and down arrows keys to go backward and forward in command history

### References 
-
