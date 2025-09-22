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
