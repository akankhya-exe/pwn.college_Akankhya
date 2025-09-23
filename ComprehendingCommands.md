# Module Name: Comprehending Commands

## Challenge Name: cat: not the pet, but the command!
Use the 'cat' command to read the file named flag inside the home directory

### Solve
**Flag:** `pwn.college{YsMU-N5n6i_Y1OJiapcOt4saumQ.QXxcTN0wyN5AzNzEzW}`

The flag file needs to be located and read inside the home directory. To locate the file, since it's in the current directory just cat flag works (relative path), or to give the full path cat ~/flag

```bash
cat flag
pwn.college{YsMU-N5n6i_Y1OJiapcOt4saumQ.QXxcTN0wyN5AzNzEzW}
```

### New Learnings
cat is used to read file contents, cat command can take multiple arguments also

### References 
-










## Challenge Name: catting absolute paths
Read a file using the cat command except the file isn't in the home directory anymore, it's in the absolute path /flag

### Solve
**Flag:** `pwn.college{sz6c4HyiNc8qVmsnTKWLa9VAYhj.QX5ETO0wyN5AzNzEzW}`

The challenge clearly states the file is located at the absolute path /flag, to read the file the command would therefore be cat /flag

```bash
cat /flag
pwn.college{sz6c4HyiNc8qVmsnTKWLa9VAYhj.QX5ETO0wyN5AzNzEzW}
```

### New Learnings
cat can be used with both relative and absolute paths depending on the current location

### References 
-









## Challenge Name: more catting practice
Read a flag that's in another directory, cannot use cd

### Solve
**Flag:** `pwn.college{YZ-qZQGkbVRpy6Y_3l8EP4G-xon.QXwITO0wyN5AzNzEzW}`

The prompt says the flag is in /usr/share/seabios/flag and to read the flag file but not to use cd, therefore to simply read the file its entire path has to be provided to cat, cat /usr/share/seabios/flag so the file can be read without going into the directory

```bash
cat /usr/share/seabios/flag
pwn.college{YZ-qZQGkbVRpy6Y_3l8EP4G-xon.QXwITO0wyN5AzNzEzW}
```

### New Learnings
cat can be used to read files in other directories using absolute paths, not a necessity to be in the directory itself

### References 
-









## Challenge Name: grepping for a needle in a haystack
Invoke the grep command to search for the required content inside a file

### Solve
**Flag:** `pwn.college{Q4CJ3ZScTRTjcejAstB6QzFo8JQ.QX3EDO0wyN5AzNzEzW}`

The actual /challenge/data.txt file has loads of irrelevant text, hence grep can be used as a search function to get the required flag, here grep will use two arguments: the substring to be searched for and the path, therefore the command is grep pwn.college /challenge/data.txt (pwn.college is in every flag)

```bash
grep pwn.college /challenge/data.txt
pwn.college{Q4CJ3ZScTRTjcejAstB6QzFo8JQ.QX3EDO0wyN5AzNzEzW}
```

### New Learnings
The grep command is used to search for required content and acts as a search filter, any substring can be searched for in any file with the correct path given

### References 
-









## Challenge Name: comparing files
The challenge consists of two almost identical files but only one of them has the real flag, it's inefficient to manually look for differences between both files, the diff command can be invoked to find the difference between both files

### Solve
**Flag:** `pwn.college{Ytj_w9yHcF9PmdmKFoJ5yjKS3v3.01MwMDOxwyN5AzNzEzW}`

Since the challenge says there is only line of difference between the decay and real file, invoking diff should output only the "difference" line which is the real flag, so diff /challenge/decoys_only.txt /challenge/decoys_and_real.txt should output only the extra line in the 2nd file which is the flag

```bash
diff /challenge/decoys_only.txt /challenge/decoys_and_real.txt
4a5
> pwn.college{Ytj_w9yHcF9PmdmKFoJ5yjKS3v3.01MwMDOxwyN5AzNzEzW}
```

### New Learnings
The diff command is used to find differences in the content of files, first it outputs the differing lines (eg, 4a5) which indicates the line where the differences are, it can detect differences in content in the same line number (replacements, eg 2c2) and additional lines (eg, 4a5)
c-change, a-addtional

### References 
-









## Challenge Name: listing files
Directories can have a lot of files which obviously cannot be manually tracked or remembered, the ls command is used to list out the content of directories

### Solve
**Flag:** `pwn.college{gWPXuwI3CUaBGYgLgcpvAOWm_Vn.QX4IDO0wyN5AzNzEzW}`

On running ls /challenge, the shell shows that there is one file called 349-renamed-run-6476 which is the required renamed run file, hence ls is used to list out files in a directory and look for required files

```bash
ls /challenge
349-renamed-run-6476  DESCRIPTION.md
/challenge/349-renamed-run-6476
Yahaha, you found me! Here is your flag:
pwn.college{gWPXuwI3CUaBGYgLgcpvAOWm_Vn.QX4IDO0wyN5AzNzEzW}
```

### New Learnings
The ls command is used to list out all files under a directory given in in its argument (ls /path) and in the current directory if there's no argument

### References 
-









## Challenge Name: touching files
The touch command is introduced to create files

### Solve
**Flag:** `pwn.college{UwmIEeYC9GtX8KHW4doRIu9CwA7.QXwMDO0wyN5AzNzEzW}`

The touch command is used to create blank files by providing the file name with the path, the challenge says to create pwn and college files in the tmp directory so /tmp/pwn and /tmp/college are the required arguments (file paths) for the touch command

```bash
cd /tmp
/tmp$ touch pwn
/tmp$ touch college
/tmp$ ls
bin  college  hsperfdata_root  pwn  tmp.TpSOPGOVKK
/tmp$ /challenge/run
Success! Here is your flag:
pwn.college{UwmIEeYC9GtX8KHW4doRIu9CwA7.QXwMDO0wyN5AzNzEzW}
```

### New Learnings
The touch command is used with its file name in the path to create new blank files

### References 
-









## Challenge Name: removing files
The rm command is introduced to remove files

### Solve
**Flag:** `pwn.college{4ROTivHk_xg6Ec_KTZ3FnnqYCM0.QX2kDM1wyN5AzNzEzW}`

As per the challenge, the delete_me file in the home directory needs to be deleted, so the command is rm delete_me, relative path is used here as the file is in the home directory itself

```bash
rm delete_me
/challenge/check
Excellent removal. Here is your reward:
pwn.college{4ROTivHk_xg6Ec_KTZ3FnnqYCM0.QX2kDM1wyN5AzNzEzW}
```

### New Learnings
The rm command along with the path as argument is used to remove files

### References 
-









## Challenge Name: moving files
Introduces the mv command which is used to move one file to another file destination

### Solve
**Flag:** `pwn.college{MGLrGd7XHJdwo70APyCSwXgQnAx.0VOxEzNxwyN5AzNzEzW}`

The challenge requires the usage of the mv (move) command to move the /flag file into /tmp/hack-the-planet (mv source destination) so the required command is mv /flag /tmp/hack-the-planet.

```bash
mv /flag /tmp/hack-the-planet
Correct! Performing 'mv /flag /tmp/hack-the-planet'.
/challenge/check
Congrats! You successfully moved the flag to /tmp/hack-the-planet! Here it is:
pwn.college{MGLrGd7XHJdwo70APyCSwXgQnAx.0VOxEzNxwyN5AzNzEzW}
```

### New Learnings
The mv command is used to move files from source to destination by specifying both path paths as arguments

### References 
-









## Challenge Name: hidden files
Files that start with . are hidden and do not show up wiht the default command, ls -a shows all the files preceding with dots and hence hidden files are available

### Solve
**Flag:** `pwn.college{YTem-cuf8Wh0jTaPfY_Bg67-Any.QXwUDO0wyN5AzNzEzW}`

Just ls does not work, therefore ls -a is needed to show all the files including hidden ones, ls -a / shows all the files in the current directory (root)
The output shows a bunch of files and one specific file that starts with . and has the word flag in its name which must be the hidden flag file
To access the file cat command is used

```bash
ls -a /
.   .dockerenv            bin   challenge  etc   lib    lib64   media  nix  proc  run   srv  tmp  var
..  .flag-10501261829219  boot  dev        home  lib32  libx32  mnt    opt  root  sbin  sys  usr
cat /.flag-10501261829219
pwn.college{YTem-cuf8Wh0jTaPfY_Bg67-Any.QXwUDO0wyN5AzNzEzW}
```

### New Learnings
Not all files show up with the ls command, hence hidden files can be accessed with the ls -a command followed by the directory path

### References 
-









## Challenge Name: An Epic Filesystem Quest
This challenge is a multi-step hunt to find the flag by using clues in multiple directories scattered across files and hidden files, demonstrating the usage of ls, cd, cat and ls -a.

### Solve
**Flag:** `pwn.college{gak9--1F59gktVgSl3u7b_6AiDE.QX5IDO0wyN5AzNzEzW}`

The challenge has two three repitive steps essentially:
1. Finding the directory in which the next clue is hidden: using cd to change to the directory that the hint leads to
2. Using ls to look for files along the lines of 'HINT' or 'CLUE' etc., in case the clue says the file is hidden then using ls -a in the directory to look for hidden files like '.MESSAGE', then the file can be read using the cat command to find the next clue
3. In case a hint says a directory is trapped, the directory cannot be accessed using cd, so ls can be used with the directory's full absolute path to list out all its files without ever needing to go into the directory so ls/absolute_path shows all the files along with the hint files
Then cat command can be used to access the necessary file as seen in the output of ls by doing ls/absolute_path/next_clue
Thus a file can be accessed without ever needing to go into the directory

```bash
hacker@commands~an-epic-filesystem-quest:~$ cd /
hacker@commands~an-epic-filesystem-quest:/$ ls
TRACE  boot       dev  flag  lib    lib64   media  nix  proc  run   srv  tmp  var
bin    challenge  etc  home  lib32  libx32  mnt    opt  root  sbin  sys  usr
hacker@commands~an-epic-filesystem-quest:/$ cat ./TRACE
Great sleuthing!
The next clue is in: /opt/linux/linux-5.4/drivers/clk/pxa

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:/$ cd /opt/linux/linux-5.4/drivers/clk/pxa
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/drivers/clk/pxa$ ls
LEAD  Makefile  clk-pxa.c  clk-pxa.h  clk-pxa25x.c  clk-pxa27x.c  clk-pxa3xx.c
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/drivers/clk/pxa$ cat ./LEAD
Congratulations, you found the clue!
The next clue is in: /opt/busybox/busybox-1.33.2/testsuite/ls

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/drivers/clk/pxa$ cd /opt/busybox/busybox-1.33.2/testsuite/ls
hacker@commands~an-epic-filesystem-quest:/opt/busybox/busybox-1.33.2/testsuite/ls$ ls -a
.  ..  .MESSAGE  ls-1-works  ls-h-works  ls-l-works  ls-s-works
hacker@commands~an-epic-filesystem-quest:/opt/busybox/busybox-1.33.2/testsuite/ls$ cat ./.MESSAGE
Congratulations, you found the clue!
The next clue is in: /opt/linux/linux-5.4/tools/perf/tests/attr

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
hacker@commands~an-epic-filesystem-quest:/opt/busybox/busybox-1.33.2/testsuite/ls$ cd /opt/linux/linux-5.4/tools/perf/tests/attr
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/tools/perf/tests/attr$ ls -a
.                              test-record-branch-filter-any_call  test-record-graph-dwarf     test-stat-C0
..                             test-record-branch-filter-any_ret   test-record-graph-fp        test-stat-basic
.INSIGHT                       test-record-branch-filter-hv        test-record-group           test-stat-default
README                         test-record-branch-filter-ind_call  test-record-group-sampling  test-stat-detailed-1
base-record                    test-record-branch-filter-k         test-record-group1          test-stat-detailed-2
base-stat                      test-record-branch-filter-u         test-record-no-buffering    test-stat-detailed-3
test-record-C0                 test-record-count                   test-record-no-inherit      test-stat-group
test-record-basic              test-record-data                    test-record-no-samples      test-stat-group1
test-record-branch-any         test-record-freq                    test-record-period          test-stat-no-inherit
test-record-branch-filter-any  test-record-graph-default           test-record-raw
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/tools/perf/tests/attr$ cat ./.INSIGHT
Congratulations, you found the clue!
The next clue is in: /usr/share/doc/bison/examples/c/rpcalc
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/tools/perf/tests/attr$ cd /usr/share/doc/bison/examples/c/rpcalc
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/bison/examples/c/rpcalc$ ls
Makefile  WHISPER  rpcalc.y
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/bison/examples/c/rpcalc$ cat ./WHISPER
Tubular find!
The next clue is in: /usr/share/javascript/mathjax/unpacked/jax/output/HTML-CSS/fonts/Neo-Euler/Arrows/Regular

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/bison/examples/c/rpcalc$ ls /usr/share/javascript/mathjax/unpacked/jax/output/HTML-CSS/fonts/Neo-Euler/Arrows/Regular
INFO-TRAPPED  Main.js
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/bison/examples/c/rpcalc$ cat /usr/share/javascript/mathjax/unpacked/jax/output/HTML-CSS/fonts/Neo-Euler/Arrows/Regular/INFO-TRAPPED
Great sleuthing!
The next clue is in: /usr/share/racket/pkgs/racket-doc/scribblings/foreign

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/bison/examples/c/rpcalc$ ls  /usr/share/racket/pkgs/racket-doc/scribblings/foreign
DISPATCH-TRAPPED        com-common.rkt   cvector.scrbl  info.rkt     os-thread.scrbl          types.scrbl
active-x.scrbl          com-intf.scrbl   define.scrbl   intro.scrbl  pointers.scrbl           unexported.scrbl
alloc.scrbl             com.scrbl        derived.scrbl  libs.scrbl   port.scrbl               utils.rkt
atomic.scrbl            compiled         file.scrbl     misc.scrbl   schedule.scrbl           vector.scrbl
collect-callback.scrbl  cpointer.scrbl   foreign.scrbl  ns.scrbl     serialize-cstruct.scrbl  winapi.scrbl
com-auto.scrbl          custodian.scrbl  global.scrbl   objc.scrbl   try-atomic.scrbl
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/bison/examples/c/rpcalc$ cat /usr/share/racket/pkgs/racket-doc/scribblings/foreign/DISPATCH-TRAPPED
Lucky listing!
The next clue is in: /usr/share/racket/pkgs/gui-doc/mrlib/scribblings/aligned-pasteboard
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/bison/examples/c/rpcalc$ cd /usr/share/racket/pkgs/gui-doc/mrlib/scribblings/aligned-pasteboard
hacker@commands~an-epic-filesystem-quest:/usr/share/racket/pkgs/gui-doc/mrlib/scribblings/aligned-pasteboard$ ls
HINT                               aligned-pasteboard-parent-intf.scrbl  horizontal-pasteboard-class.scrbl
aligned-editor-canvas-class.scrbl  aligned-pasteboard.scrbl              stretchable-snip-intf.scrbl
aligned-editor-snip-class.scrbl    common.rkt                            vertical-pasteboard-class.scrbl
aligned-pasteboard-intf.scrbl      compiled
hacker@commands~an-epic-filesystem-quest:/usr/share/racket/pkgs/gui-doc/mrlib/scribblings/aligned-pasteboard$ cat ./HINT
Yahaha, you found me!
The next clue is in: /opt/linux/linux-5.4/include/config/dmi/scan/machine/non/efi
hacker@commands~an-epic-filesystem-quest:/usr/share/racket/pkgs/gui-doc/mrlib/scribblings/aligned-pasteboard$ cd /opt/linux/linux-5.4/include/config/dmi/scan/machine/non/efi
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/include/config/dmi/scan/machine/non/efi$ ls
NOTE  fallback.h
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/include/config/dmi/scan/machine/non/efi$ cat ./NOTE
CONGRATULATIONS! Your perserverence has paid off, and you have found the flag!
It is: pwn.college{gak9--1F59gktVgSl3u7b_6AiDE.QX5IDO0wyN5AzNzEzW}
```

### New Learnings
The main learning was remote interacting and the usage of absolute paths along with some practice of ls and ls -a to access files remotely using full absolute paths in order to bypass the need to keep switching directories, by using ls and cat with full absolute paths files can be inspected and read from anywhere on the system

### References 
-
