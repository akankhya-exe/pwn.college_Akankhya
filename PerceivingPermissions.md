# Module Name: Perceiving Permissions

## Challenge Name: Changing File Ownership
The challenge is to change ownership of the /flag file to the hacker user using chown and accessing the flag from the hacker user's permissions.

### Solve
**Flag:** `pwn.college{QW5DWfDZpCDpa8M5jdolDdxFErL.QXxEjN0wyN5AzNzEzW}`

Before changing ownership the /flag wile is under the root user which is not accessible for this particular challenge. By using chown [user] [file] the file can be transffered under the hacker user's name.
So chown hacker /flag puts the /flag file under the hacker user (as seen in the output of ls -l) from where the flag can be accessed with the same privileges as the root user.

```bash
chown hacker /flag
ls -l
total 32
-rw-r--r-- 1 hacker hacker   4 Sep 24 17:23 COLLEGE
-rw-r--r-- 1 hacker hacker   8 Sep 24 18:10 PWN
-rw-r--r-- 1 root   hacker  60 Sep 22 15:06 a
-rw-r--r-- 1 root   hacker  77 Sep 25 13:38 bug
-rw-r--r-- 1 hacker hacker 829 Sep 24 17:48 instructions
-rw-r--r-- 1 hacker hacker  95 Sep 24 17:48 myflag
lrwxrwxrwx 1 hacker hacker   5 Sep 23 10:41 not-the-flag -> /flag
-rw-r--r-- 1 hacker hacker 437 Sep 24 17:41 the-flag

cat /flag
pwn.college{QW5DWfDZpCDpa8M5jdolDdxFErL.QXxEjN0wyN5AzNzEzW}
```

### New Learnings
To change file ownership the chown [user] [file] command is used.

### References 
-









## Challenge Name: Groups and Files
The /flag file is present in a group that the user (hacker) is not a part of, first the ownership of the flag has to be changed to a group the user is a part of and then read.

### Solve
**Flag:** `pwn.college{YwioOHUCRu7zkfiELvuWlzuJzzJ.QXxcjM1wyN5AzNzEzW}`

Using id to check what groups the user is a part of (only hacker group and the id is 1000), using chgrp [grp] [file] the file group ownership can be changed. So, chgrp hacker /flag to give access of the /flag file to the hacker group.
Then use cat to read the flag.

```bash
id
uid=1000(hacker) gid=1000(hacker) groups=1000(hacker)

chgrp hacker /flag
cat /flag
pwn.college{YwioOHUCRu7zkfiELvuWlzuJzzJ.QXxcjM1wyN5AzNzEzW}
```

### New Learnings
Files are owned by both users and groups. The id command is used to check the current user's id and what groups they're a part of. chgrp is used to change a file's group ownership.

### References 
-









## Challenge Name: Fun With Groups Name
Previously, the user is in a group with the same name (common convention) but this time the hacker user's group name has been changed and needs to be found first in order to transfer /flag file ownership to access it.

### Solve
**Flag:** `pwn.college{cD70vlASmEnJaV9wLmrft4mxlwf.QXycjM1wyN5AzNzEzW}`

To view all groups a user is a part of use command id. Clearly, the user is a part of the group called grp3944. To change ownership of the /flag file: chgroup grp3944 /flag. And then cat to read it.

```bash
id
uid=1000(hacker) gid=1000(grp3944) groups=1000(grp3944)
chgrp grp3944 /flag
cat /flag
pwn.college{cD70vlASmEnJaV9wLmrft4mxlwf.QXycjM1wyN5AzNzEzW}
```

### New Learnings
A user can be a part of multiple groups, and the group names do not have to match the user name.

### References 
-









## Challenge Name: Changing Permissions
The challenge is to read the /flag file owned by the root user, need to use chmod to change permissions to give access to other users to be able to read the file. The ownership cannot be changed but special permissions can be given.

### Solve
**Flag:** `pwn.college{ohqS1CEwT6r7b4Cj_99kAaL8aAT.QXzcjM1wyN5AzNzEzW}`

File permissions have three categories:
u: owner of the file
g: group that owns the file
o: every other user

For each of these three, there are three permission types:
r: read the contents and list in a directory
w: permission to modify file, add/delete in a directory
x: execute the file, cd into a directory

+ to add permissions, - to remove permissions

On doing ls -l /flag: -r-------- is the output meaning only the owner can read the file, no one else can read the file. The hacker user falls into the other category (not part of the root group either on checking with id). 
The challenge is to give reading permissions to the hacker user so the argument would be: o+r (giving reading permissions to others)
The full command is therefore: chmod o+r /flag.

```bash
chmod o+r /flag
cat /flag
pwn.college{ohqS1CEwT6r7b4Cj_99kAaL8aAT.QXzcjM1wyN5AzNzEzW}
```

### New Learnings
File permissions and permission categories (rwx and ugo), chmod command to add or remove permissions using +, -. Permission != Ownership. Permission to modify/read a file can be given if you don't own the file.

### References 
-









## Challenge Name: Executable Files
The /challenge/run file's permissions are all with the root user. The goal is to give execution access to the hacker user to execute the program for the file.

### Solve
**Flag:** `pwn.college{gB7ASly4z3O2jizp8OgG8wW6H6k.QXyEjN0wyN5AzNzEzW}`

Starting with ls -l, the /flag required file is owned by the hacker user and the hacker group, so only group or user permissions need to be changed (u or g). Since execution perm needs to be given the entire command is +x /challenge/run (not writing something before +x automatically changes the group perms).
[Did o+x first but permission was denied as hacker is part of the hacker group that owns the file already, not part of the 'others' category]

```bash
ls -l
lrwxrwxrwx 1 hacker hacker   5 Sep 23 10:41 not-the-flag -> /flag

chmod +x /challenge/run
/challenge/run
Successful execution! Here is your flag:
pwn.college{gB7ASly4z3O2jizp8OgG8wW6H6k.QXyEjN0wyN5AzNzEzW}
```

### New Learnings
Practical usage of cmod, difference between user, group and other perms.

### References 
-









## Challenge Name: Permission Tweaking Practice
There are 8 rounds of changing permissions from the current to required permissions by using chmod combinations. The changes need be to analyzed according to the 9 character permission text.

### Solve
**Flag:** `pwn.college{oGhYbHIL3KWgTZaGRa5n8xN60m-.QXwEjN0wyN5AzNzEzW}`

(Explanation for 1 as an example)
The current permission is rw-r--r--
First three bits: user
Second three bits: group
Third three bits: others
Required permission is: rwxr--r--
Clearly, the user needs to be given execution permission so the command is: chmod u+x /challenge/pwn.

```bash
 /challenge/run
Round 1 of 8!

Current permissions of "/challenge/pwn": rw-r--r--
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": rwxr--r--
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
chmod u+x /challenge/pwn

You set the correct permissions!
Round 2 of 8!

Current permissions of "/challenge/pwn": rwxr--r--
Needed permissions of "/challenge/pwn": rwxr-xr-x

chmod go+x /challenge/pwn
You set the correct permissions!
Round 3 of 8!

Current permissions of "/challenge/pwn": rwxr-xr-x
Needed permissions of "/challenge/pwn": rw-r-xr--

chmod uo-x /challenge/pwn
You set the correct permissions!
Round 4 of 8!
Current permissions of "/challenge/pwn": rw-r-xr--
Needed permissions of "/challenge/pwn": r--r--r--

chmod u-w,g-x /challenge/pwn
You set the correct permissions!
Round 5 of 8!

Current permissions of "/challenge/pwn": r--r--r--
Needed permissions of "/challenge/pwn": r--r------

chmod o-r /challenge/pwn
You set the correct permissions!
Round 6 of 8!
Needed permissions of "/challenge/pwn": ---r-----
Current permissions of "/challenge/pwn": r--r-----
chmod u-r /challenge/pwn

You set the correct permissions!
Round 7 of 8!

Current permissions of "/challenge/pwn": ---r-----
Needed permissions of "/challenge/pwn": ---rw--w-

chmod go+w /challenge/pwn
You set the correct permissions!
Round 8 of 8!
Needed permissions of "/challenge/pwn": ---------

chmod g-rw,o-w /challenge/pwn
You set the correct permissions!
You've solved all 8 rounds! I have changed the ownership
of the /flag file so that you can 'chmod' it. You won't be able to read
it until you make it readable with chmod!

chmod +r /flag
cat /flag
pwn.college{oGhYbHIL3KWgTZaGRa5n8xN60m-.QXwEjN0wyN5AzNzEzW}

```

### New Learnings
Multiple perms can be given in one command by combing user categories like go, uo etc and by separating them by commas, chmod uo+x, g-r /challenge/pwn.

### References 
-









## Challenge Name
The goal is to do a set of 8 rounds of permission changing again, except using the = operator in chmod instead of +,-

### Solve
**Flag:** `pwn.college{helloworld}`

(Example 1):
Current: rw-r--r--
Needed: -w-r----x

User needs w, so u=w (only writing permission given, overwrites everything else)
Group needs r only, so g=r
Other needs only x, so o=x
chmod u=w,g=r,o=x /challenge/pwn

```bash
 /challenge/run
Round 1 of 8!

Current permissions of "/challenge/pwn": rw-r--r--
Needed permissions of "/challenge/pwn": -w-r----x

chmod u=w,g=r,o=x /challenge/pwn
You set the correct permissions!
Round 2 of 8!

Current permissions of "/challenge/pwn": -w-r----x
Needed permissions of "/challenge/pwn": r-xrw-r--

chmod u=rx,g=rw,o=r /challenge/pwn
You set the correct permissions!
Round 3 of 8!

Current permissions of "/challenge/pwn": r-xrw-r--
Needed permissions of "/challenge/pwn": rw-rwx-wx

chmod u=rw,g=rwx,o=wx /challenge/pwn
You set the correct permissions!
Round 4 of 8!

Current permissions of "/challenge/pwn": rw-rwx-wx
Needed permissions of "/challenge/pwn": -wx-wxrw-

 chmod u=wx,g=wx,o=rw /challenge/pwn
You set the correct permissions!
Round 5 of 8!

Current permissions of "/challenge/pwn": -wx-wxrw-
Needed permissions of "/challenge/pwn": -wx--xr--
chmod u=wx,g=x,o=r /challenge/pwn
You set the correct permissions!
Round 6 of 8!

Current permissions of "/challenge/pwn": -wx--xr--
Needed permissions of "/challenge/pwn": ------rw-

chmod ug=,o=rw /challenge/pwn

You set the correct permissions!
Round 7 of 8!

Current permissions of "/challenge/pwn": ------rw-
Needed permissions of "/challenge/pwn": rw---x-wx
chmod u=rw,g=x,o=wx /challenge/pwn

You set the correct permissions!
Round 8 of 8!

Current permissions of "/challenge/pwn": rw---x-wx
Needed permissions of "/challenge/pwn": ---r-----

chmod uo=,g=r /challenge/pwn

You set the correct permissions!
You've solved all 8 rounds! I have changed the ownership
of the /flag file so that you can 'chmod' it. You won't be able to read
it until you make it readable with chmod!

chmod u=r /flag
cat /flag
pwn.college{IsMRR1sL7rQxqge9aqE8lqauUaB.QXzETO0wyN5AzNzEzW}
```

### New Learnings
= operator in chmod is used for the same purpose except it overrides every other permission other than the one specified in its argument.

### References 
-









## Challenge Name: The SUID Bit
The goal is to give root privileges by using the SUID Bit perm on /challenge/getroot program. Root shell will be granted and the flag program has to be run.

### Solve
**Flag:** `pwn.college{4Xi5w4Y9HxcyK0NJNXzaR9Qu9Ih.QXzEjN0wyN5AzNzEzW}`

The SUID Bit gives permissions to run a file with the same authorization as the user (root in this case). Command is chmod u+s /challenge/getroot. Now the shell runs as root user and program can be run to get
the flag.

```bash
command 1
command 2
pwn.college{helloworld}
```

### New Learnings
This is a special permission bit that, when set on an executable file, allows any user who runs it to execute it with the privileges of the file's owner. The command chmod u+s is used to apply the SUID permission to a file.

### References 
-
