# Module Name: Terminal Multiplexing

## Challenge Name: Launching Screen
Launch another screen to get the flag.

### Solve
**Flag:** `pwn.college{kJ2qhWgvI_QRIefElGfzc2470bt.0VN4IDOxwyN5AzNzEzW}`

Using the screen command launches another screen session that is exited by typing 'exit' on the command line.

```bash
screen
Congratulations! You're inside a screen session!
Here's your flag:
pwn.college{kJ2qhWgvI_QRIefElGfzc2470bt.0VN4IDOxwyN5AzNzEzW}
```

### New Learnings
screen creates virtual terminals inside the terminal, allows opening multiple windows.

### References 
-









## Challenge Name
The goal is open a new screen, detach from it and then run the program that gives the flag and reattach to get the flag output.

### Solve
**Flag:** ` pwn.college{YS1W1fZq23I6289H-8zQ_NMVjrO.0lN4IDOxwyN5AzNzEzW}`

To start a session: screen
Press Ctrl + A followed by d to detach.
Run /challenge/run
Use screen -r to reattach to the screen.

```bash
screen
[detached from 154.pts-1.terminal-multiplexing~detaching-and-attaching]
/challenge/run
Found detached screen session: 154.pts-1.terminal-multiplexing~detaching-and-attaching
Sending flag to your screen session...

Flag sent! Now reattach to your screen session with:

  screen -r

You'll find the flag waiting for you there!

screen -r
hacker@terminal-multiplexing~detaching-and-attaching:~$ echo Yes! Flag is: pwn.college{YS1W1fZq23I6289H-8zQ_NMVjrO.0lN4IDOxwyN5AzNzEzW}
Yes! Flag is: pwn.college{YS1W1fZq23I6289H-8zQ_NMVjrO.0lN4IDOxwyN5AzNzEzW}
```

### New Learnings
Ctrl + A + d to detach from a screen, screen -r to reattach to a screen.

### References 
-









## Challenge Name
The goal is to find the session with the real flag out of multiple decoy sessions by detaching and reattaching to them.

### Solve
**Flag:** `pwn.college{4c1yqMH-JIQw5kqV419ULRTSVXe.01N4IDOxwyN5AzNzEzW}`

Firt execute -ls to find all running sessions. Clear the 144, 147 and 150 ones are of interest. Start attaching to each one by screen -r <session name>, the new screen will display the flag (the last one is the real flag containing session)
otherwise contains a decoy message. Keep using screen -r and Ctrl + A + d to reattach and detach to screens to find the real one.

```bash
screen -ls
There are screens on:
        149.pts-0.terminal-multiplexing~launching-screen        (Remote or dead)
        139.pts-0.terminal-multiplexing~detaching-and-attaching (Remote or dead)
        154.pts-1.terminal-multiplexing~detaching-and-attaching (Remote or dead)
        144.session_f19984bdf40b8efa    (Remote or dead)
        147.session_0aebe2b860b5a19c    (Remote or dead)
        150.session_67d7a6c3eff83f65    (Remote or dead)
        144.session_4f5aea05ecab95fc    (Detached)
        147.session_186de7c4301475b8    (Detached)
        150.session_3b0bee308f9df25e    (Detached)
9 Sockets in /home/hacker/.screen.
hacker@terminal-multiplexing~finding-sessions:~$  echo 'Congratulations! You found the right session!'
Congratulations! You found the right session!
hacker@terminal-multiplexing~finding-sessions:~$  echo pwn.college{4c1yqMH-JIQw5kqV419ULRTSVXe.01N4IDOxwyN5AzNzEzW}

screen -r 144.session_4f5aea05ecab95fc
[detached from 144.session_4f5aea05ecab95fc]

screen -r 147.session_186de7c4301475b8
[detached from 147.session_186de7c4301475b8]

screen -r 150.session_3b0bee308f9df25e
[detached from 150.session_3b0bee308f9df25e]
```

### New Learnings
To list all sessions: screen -ls
Managing multiple sessions by reattaching with screen -r <name> and detaching with Ctrl + A + d to work with different sessions.

### References 
-









## Challenge Name: Switching Windows
The goal is to navigate between different windows inside a screen session, need to try switching between preset windows numbered 0, 1 etc to find the flag.

### Solve
**Flag:** `pwn.college{8xOG2iPtkV7J8zgXQLNdxlQNhyk.0FO4IDOxwyN5AzNzEzW}`

First attach to the screen using screen -r
The window clearly states the flag is in window 0.
Use Ctrl + A + 0 to switch to window 0 (Ctrl + A + x is the way to switch to the x window). Flag is found.

```bash
screen -r
cat <<MSG
Welcome to the window switching challenge!
You are currently in window 1.
The flag is hidden in window 0.
Use Ctrl-A 0 to switch to window 0!
MSG

Ctrl + A + 0

cat <<MSG
> Excellent work! You found window 0!
> Here is your flag: pwn.college{8xOG2iPtkV7J8zgXQLNdxlQNhyk.0FO4IDOxwyN5AzNzEzW}
> MSG
```

### New Learnings
Ctrl + A + (0-9) is used to go through all windows by their number. Multiple windows can be in a same screen session.

### References 
-









## Challenge Name: Detaching and Attaching (tmux)
The goal is to practice attaching and detaching to a tmux terminal and then reattaching.

### Solve
**Flag:** `pwn.college{QHFDKJzVdp3lFkE7UOqeqVTOzcC.0VO4IDOxwyN5AzNzEzW}`

According to the question, first attach to the mux terminal by using tmux. Secondly, detach using ctrl + B + d. Third, run /challenge/run and then use tmux attach to reatach to find the flag in the window.

```bash
tmux
Ctrl + B + d
[detached (from session 0)]
/challenge/run
Found detached tmux session: 0
Sending flag to your tmux session...

Flag sent! Now reattach to your tmux session with:
  tmux attach

You'll find the flag waiting for you there!

tmux a
echo Congratulations, here is your flag: pwn.college{QHFDKJzVdp3lFkE7UOqeqVTOzcC.0VO4IDOxwyN5AzNzEzW}
```

### New Learnings
Managing terminals, detaching and attaching to mux terminals.

### References 
-









## Challenge Name: Switching Windows (tmux)
The goal is to navigate between windows by using Ctrl + B + (0-9), flip to window 0 to find the flag.

### Solve
**Flag:** `pwn.college{Uk4CbM2bFP_kT4aDfYi0n25XX86.0FM5IDOxwyN5AzNzEzW`

[Do NOT do tmux after opening the terminal, it creates a completely new terminal with no windows in it, that's why Ctrl + B + 0 after doing tmux wasn't working, on launching the challenge the tmux environment is already set up]
Use tmux ls to find all active sessions, clearly challenge_session is the active session with two windows.
Attach to it by using tmux attach -t challenge_session
Then use Ctrl + B + 0 to switch to window 0.

```bash
tmux ls

challenge_session: 2 windows (created Tue Sep 30 15:22:42 2025)

tmux attach -t challenge_session
cat <<MSG
> Excellent work! You found window 0!
> Here is your flag: pwn.college{Uk4CbM2bFP_kT4aDfYi0n25XX86.0FM5IDOxwyN5AzNzEzW}
> MSG
```

### New Learnings
tmux uses modern command structure like ls, attach compared to screen -r etc.

### References 
-
