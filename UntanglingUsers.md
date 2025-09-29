# Module Name: Untangling Users

## Challenge Name: Becoming root with su
The goal is to switch to the root user by providing the correct password for authentication and then read the flag.

### Solve
**Flag:** `pwn.college{cgljihFY-STHT_vKdJrkJXPMPv_.QX1UDN1wyN5AzNzEzW}`

To switch to root user the command is su, this will prompt for a password which is given in the question as hack-the-planet. The user will then switch from hacker to root. On doing ls -l it can be seen that the /not-the-flag file is highlighted and contains the flag which can be read using a simple cat.

```bash
su
Password: hack-the-planet
root@users~becoming-root-with-su:/home/hacker# ls -l
total 32
-rw-r--r-- 1 hacker hacker   4 Sep 24 17:23 COLLEGE
-rw-r--r-- 1 hacker hacker   8 Sep 24 18:10 PWN
-rw-r--r-- 1 root   hacker  60 Sep 22 15:06 a
-rw-r--r-- 1 root   hacker  77 Sep 25 13:38 bug
-rw-r--r-- 1 hacker hacker 829 Sep 24 17:48 instructions
-rw-r--r-- 1 hacker hacker  95 Sep 24 17:48 myflag
lrwxrwxrwx 1 hacker hacker   5 Sep 23 10:41 not-the-flag -> /flag
-rw-r--r-- 1 hacker hacker 437 Sep 24 17:41 the-flag
root@users~becoming-root-with-su:/home/hacker# cat ./not-the-flag
pwn.college{cgljihFY-STHT_vKdJrkJXPMPv_.QX1UDN1wyN5AzNzEzW}

```

### New Learnings
su (an older utility) is used to gain the root user authorization with the help of some aunthentication, here it is a password.

### References 
-









## Challenge Name: Other users with su
The challenge is to switch to another user zardus using the su command and then get the flag from there as the zardus user.

### Solve
**Flag:** `pwn.college{oN7PFRsQ-ecQRKJpQkLWor6aoqs.QX2UDN1wyN5AzNzEzW}`

To switch to another user (su without any argument is default root user) add the user's name after the su command so: su <user>

```bash
su zardus
Password: dont-hack-me
zardus@users~other-users-with-su:/home/hacker$ /challenge/run
Congratulations, you have become Zardus! Here is your flag:
pwn.college{oN7PFRsQ-ecQRKJpQkLWor6aoqs.QX2UDN1wyN5AzNzEzW}
```

### New Learnings
su can be used to switch to root user and other users too.

### References 
-









## Challenge Name: Cracking passwords
The challenge is to use the John the Ripper program to crack the /etc/shadow (leaked) file, get the password for the zardus user and get the flag.

### Solve
**Flag:** `pwn.college{M6LBmYMkNciLehmKhDz8c9zlZCu.QX3UDN1wyN5AzNzEzW}`

The leaked file is /challenge/shadow-leak as given in the question, using it with john starts cracking the files. After john finishes, the cracked passwords can be shown using john --show, the password for the zardus user is given.
Switch to zardus user using su and then use the cracked password found using john ('aardvark'). Then retrieve the flag.

```bash
john /challenge/shadow-leak
Created directory: /home/hacker/.john
Loaded 1 password hash (crypt, generic crypt(3) [?/64])
Press 'q' or Ctrl-C to abort, almost any other key for status
0g 0:00:00:11 0% 2/3 0g/s 270.8p/s 270.8c/s 270.8C/s piglet..knight
aardvark         (zardus)
1g 0:00:00:21 100% 2/3 0.04699g/s 273.6p/s 273.6c/s 273.6C/s Johnson..buzz
Use the "--show" option to display all of the cracked passwords reliably
Session completed

john --show /challenge/shadow-leak
hacker:NO PASSWORD:20357:0:99999:7:::
zardus:aardvark:20360:0:99999:7:::

2 password hashes cracked, 0 left

su zardus
Password: aardvark

/challenge/run
Congratulations, you have become Zardus! Here is your flag:
pwn.college{M6LBmYMkNciLehmKhDz8c9zlZCu.QX3UDN1wyN5AzNzEzW}
```

### New Learnings
Linux stores hashed passwords (can't be reversed) in the /etc/shadow file hence protecting it is critical. The john command is used to "crack" passwords by trying loads of hashed combinations and tries to match
them to the hashed passwords in the /etc/shadow file until it finds a match. Then john --show can be used to show all successful matches in a normal readable format. 

### References 
https://www.esecurityplanet.com/products/john-the-ripper/ (Understanding john)









## Challenge Name: Using sudo
The goal is to read the flag (execute the command) with root privileges using sudo.

### Solve
**Flag:** `pwn.college{wQQD9WOu9cNmFPQBN50R5KrP7fO.QX4UDN1wyN5AzNzEzW}`

Using sudo defaults to running as the root user, so the flag has to be read as normal except sudo command has to be used before it, using sudo ls -l all the files can be seen in the root user's current directory.
Clearly, sudo cat ./not-the-flag will give the flag by using root privileges.

```bash
sudo ls -l
total 32
-rw-r--r-- 1 hacker hacker   4 Sep 24 17:23 COLLEGE
-rw-r--r-- 1 hacker hacker   8 Sep 24 18:10 PWN
-rw-r--r-- 1 root   hacker  60 Sep 22 15:06 a
-rw-r--r-- 1 root   hacker  77 Sep 25 13:38 bug
-rw-r--r-- 1 hacker hacker 829 Sep 24 17:48 instructions
-rw-r--r-- 1 hacker hacker  95 Sep 24 17:48 myflag
lrwxrwxrwx 1 hacker hacker   5 Sep 23 10:41 not-the-flag -> /flag
-rw-r--r-- 1 hacker hacker 437 Sep 24 17:41 the-flag

sudo cat ./not-the-flag
pwn.college{wQQD9WOu9cNmFPQBN50R5KrP7fO.QX4UDN1wyN5AzNzEzW}
```

### New Learnings
sudo is used to execute commands with the privileges of another user (usually root). su switches to the other user's shell entire by using a password, sudo runs a command as another user by checking the /etc/sudoers file, used for temporary privileges.

### References 
-
