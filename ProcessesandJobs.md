# Module Name: Processes and Jobs

## Challenge Name: Listing Processes
The goal is to find the /challenge/run file but it cannot be accessed using ls and can only be accessed by looking at all running processes.

### Solve
**Flag:** `pwn.college{IcMIyNlDwftX8TasbJk8Cq9AioQ.QX4MDO0wyN5AzNzEzW}`

According to the question, the /challenge/run file will be displayed when displaying all the running processes. To show all running processes the command is ps -ef which shows each and every full process on the terminal.
In the output /challenge/6615-run-4988 file is accessible.

```bash
ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 14:39 ?        00:00:00 /sbin/docker-init -- /nix/var/nix/profiles/dojo-workspace/bin/dojo-i
root           7       1  0 14:39 ?        00:00:00 /run/dojo/bin/sleep 6h
root         132       1  0 14:39 ?        00:00:00 /challenge/6615-run-4988

/challenge/6615-run-4988
Yahaha, you found me! Here is your flag:
pwn.college{IcMIyNlDwftX8TasbJk8Cq9AioQ.QX4MDO0wyN5AzNzEzW}
```

### New Learnings
ps - used to list and inspect current running processes
Each process has attributes like PID and a full command to launch
ps -ef is used to see all systemwide processes

### References 
-









## Challenge Name: Killing Processes
The goal is to retrieve the flag from /challenge/run, except it will not run until /challenge/dont_run is still up and running, it has to be killed (terminated) before using /challenge/run.

### Solve
**Flag:** `pwn.college{M6jcmo22FLVwlq9aadxAYjOGlSJ.QXyQDO0wyN5AzNzEzW}`

Using ps -e to find all the running processes first, clearly sleep cmd is prohibiting the running of /challenge/run. kill with PID has to be used to terminate a command, PID of sleep is 137 so kill 137 kills the sleep commnand and /challenge/run can be run.

```bash
ps -e
    PID TTY          TIME CMD
      1 ?        00:00:00 docker-init
      7 ?        00:00:00 /run/dojo/bin/s
    135 ?        00:00:00 su
    136 ?        00:00:00 bash
    137 ?        00:00:00 sleep

kill 137
hacker@processes~killing-processes:~$ /challenge/run
Great job! Here is your payment:
pwn.college{M6jcmo22FLVwlq9aadxAYjOGlSJ.QXyQDO0wyN5AzNzEzW}
```

### New Learnings
kill <PID> is used to terminate a process.

### References 
-









## Challenge Name: Interrupting Processes
The goal is to run /challenge/run but the program will not give the flag until the program is interrupted by using Ctrl + C.

### Solve
**Flag:** `pwn.college{0FaEtsOZq3ScZTL2kHdstag_Hwo.QXzQDO0wyN5AzNzEzW}`

To terminate a program the shortcut is Ctrl + C

```bash
/challenge/run
I could give you the flag... but I won't, until this process exits. Remember,
you can force me to exit with Ctrl-C. Try it now!
^C
Good job! You have used Ctrl-C to interrupt this process! Here is your flag:
pwn.college{0FaEtsOZq3ScZTL2kHdstag_Hwo.QXzQDO0wyN5AzNzEzW}
```

### New Learnings
Ctrl + C is used to exit a program by interrupting it.

### References 
-









## Challenge Name: Killing Misbehaving Processes
The goal is to stop a process /challenge/decoy that keeps spamming decoy flags into a pipe called /tmp/flag_fifo. The process needs to be killed in order to run the correct /challenge/run command to get the flag.

### Solve
**Flag:** `pwn.college{YYiOC68uuU9VEuAfyg4UjVyNVZ5.0FNzMDOxwyN5AzNzEzW}`

First step is setting up the pipe's "listening" mechanism cat /tmp/flag_fifo (pipe is now being read, pipe exists already). Now the goal is to find the decoy process and kill it, for this we input all the processes running and grep it through a pipeline with the argument decoy to find the decoy process that is spamming useless flags.
So: ps -ef | grep decoy
Next is killing the decoy using kill <PSID>
Lastly run actual /challenge/run

```bash
cat /tmp/flag_fifo
mkfifo: cannot create fifo '/tmp/flag_fifo': File exists
pwn.college{sfYGbijcUEQZcmKiSpiceHtycIFKNUkfLn97d5VCH6YSXB-}
pwn.college{sKwUaCqhfb8jRpYWkJn4X59C1wAiZwrafzkoS7DqZDUSyvZ}
pwn.college{oGDmlmHF4O9hQRX6h0wrdK1MTIO.D7b6Ot8KneYrvcoSAoM}
pwn.college{lLrxkf66eaolOc4pLkx-buvF09c1Sfsbj2KtOSLCVK4T9F9}
pwn.college{Z2m.QUFbs69I9YXlN2NGbfBkAa96K02n4JK99JZIuoUSaUG}
...

ps -ef | grep decoy
hacker       167     150  0 15:42 pts/0    00:00:00 grep --color=auto decoy

kill 167

/challenge/run
Sending the flag to /tmp/flag_fifo!

cat /tmp/flag_fifo
pwn.college{YYiOC68uuU9VEuAfyg4UjVyNVZ5.0FNzMDOxwyN5AzNzEzW}
client_loop: send disconnect: Broken pipe
```

### New Learnings
The challenge again reinforces the concept of using kill to get rid of unwanted files, even data stored in a pipe being blocked or contaminated by a foreign process can be identified using ps -ef (and grep) to terminate the program and run the pipe commands as usual.

### References 
-









## Challenge Name: Suspending processes
The goal is to run two instances of /challenge/run in the same terminal. This is achieved by suspendin the first terminal and using the second one.

### Solve
**Flag:** `pwn.college{w7ZSHtpyQfRGDYVQFIB_qBFg1YE.QX1QDO0wyN5AzNzEzW}`

Start the first program normally using /challenge/run. Using ctrl + z will suspend the program and return to the shell prompt. Running /challenge/run again runs another instance (second instance) and this is detected and the flag is retrieved.

```bash
/challenge/run
I'll only give you the flag if there's already another copy of me running in
this terminal... Let's check!

UID          PID    PPID  C STIME TTY          TIME CMD
root         168     159  0 18:40 pts/2    00:00:00 bash /challenge/run
root         170     168  0 18:40 pts/2    00:00:00 ps -f

I don't see a second me!

To pass this level, you need to suspend me and launch me again! You can
background me with Ctrl-Z or, if you're not ready to do that for whatever
reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                 /challenge/run

/challenge/run
I'll only give you the flag if there's already another copy of me running in
this terminal... Let's check!

UID          PID    PPID  C STIME TTY          TIME CMD
root         168     159  0 18:40 pts/2    00:00:00 bash /challenge/run
root         175     159  0 18:40 pts/2    00:00:00 bash /challenge/run
root         177     175  0 18:40 pts/2    00:00:00 ps -f

Yay, I found another version of me! Here is the flag:
pwn.college{w7ZSHtpyQfRGDYVQFIB_qBFg1YE.QX1QDO0wyN5AzNzEzW}
```

### New Learnings
Background problems - a process that is running or suspended but not interacting with the terminal currently
Ctrl + Z pauses the program and puts it in the background, Ctrl + C exits the program completely

### References 
-









## Challenge Name: Resuming processes
The goal is to suspend and resume a file in order to retrieve the flag.

### Solve
**Flag:** `pwn.college{0Vnaen3hUzrHeB-VqF5XXX0iTpg.QX2QDO0wyN5AzNzEzW}`

Run /challenge/run to run the program. To suspend the program do Ctrl + Z. To resume a program the command is fg.
```bash
/challenge/run
Let's practice resuming processes! Suspend me with Ctrl-Z, then resume me with
the 'fg' command! Or just press Enter to quit me!
^Z
[1]+  Stopped                 /challenge/run

fg
/challenge/run
I'm back! Here's your flag:
pwn.college{0Vnaen3hUzrHeB-VqF5XXX0iTpg.QX2QDO0wyN5AzNzEzW}
Don't forget to press Enter to quit me!
```

### New Learnings
fg is used to resume a suspended program in the foreground.

### References 
-









## Challenge Name: Backgrounding processes
Add challenge description here

### Solve
**Flag:** `pwn.college{kZcJlpL_AReomAIHBpLBM829QMV.QX3QDO0wyN5AzNzEzW}`

type in your solve and your thought process behind solving the challenge. Include as much as info as possible. Use triple ticks for any bash commands and output you type on the terminal.

```bash
/challenge/run
I'll only give you the flag if there's already another copy of me running *and
not suspended* in this terminal... Let's check!

UID          PID STAT CMD
root         153 S+   bash /challenge/run
root         155 R+   ps -o user=UID,pid,stat,cmd

I don't see a second me!

To pass this level, you need to suspend me, resume the suspended process in the
background, and then launch a new version of me! You can background me with
Ctrl-Z (and resume me in the background with 'bg') or, if you're not ready to
do that for whatever reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                 /challenge/run

bg
[1]+ /challenge/run &


/challenge/run
I'll only give you the flag if there's already another copy of me running *and
not suspended* in this terminal... Let's check!

UID          PID STAT CMD
root         153 S    bash /challenge/run
root         163 S    sleep 6h
root         164 S+   bash /challenge/run
root         166 R+   ps -o user=UID,pid,stat,cmd

Yay, I found another version of me running in the background! Here is the flag:
pwn.college{kZcJlpL_AReomAIHBpLBM829QMV.QX3QDO0wyN5AzNzEzW}

```

### New Learnings
Brief note on what you learned from the challenge

### References 
Add any references or videos you used while solving the challenge.





