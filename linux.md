[Back to Main page](README.md)

# Linux basics

### ip a
- Own ip adress

### pwd
- Print working directory

### Ctrl + L
- Scrolls terminal until it's blank

### whoami / id
- Prints current user

### cat \<filename>
- Writes out content of a file

### echo \<text>
- Write text or replace text in a file
    - if used as `echo <text> >`, replaces the whole text in the file with the text you echoed
    - if used as `echo <text> >>`, adds the text to the end of the already existing text

### ls \<directory, optional>
- Lists all files and directories
    - `-a` to view all, including hidden
    - `-l` t view details, including **permissions**

### su \<user to switch to>
- Switches users. You'll need to know their password tho

### sudo \<command> \<modifier>
- Super User DO. Run something with elevated privileges. You'll need the current user's password
- The modifier `-u <user>` is useful here, letting you run commands or programs as other users, without switching to them 
    - important, you need to have permission to run that command/program to do this

### locate \<filename+extension>
- Locates a specific file on your computer

## Permissions

```
    $ ls -l
    drwxr-xr-x. 4 root root    68 Jun 13 20:25 tuned
    -rw-r--r--. 1 root root  4017 Feb 24  2022 vimrc
```

Every file in linux has a something like `-rw-r--r--. 1 root root`. 

- What we're interested in is `rw-r--r--` (without the first - or letter)
    - It can be divided into 3 parts: `rw-`, `r--`, `r--`
    - The first set of permissions applies to the owner of the file. The second set of permissions applies to the user group that owns the file. The third set of permissions is generally referred to as "others."
    - The first and second `root` after the permissions part refers to the user and group owner of the file

### Changing permissions

### chmod \<filename>
- It is used to change permissions of a file. This can be done in two ways:
    - Numbers: the read permission represents `4`, write `2`, and execute `1`. Added together they represent the permissions.
        - 3 of these numbers together form the full permissions for a file (first number for the owner, second for the group, third for "others")
        - eg. `chmod 777 <filename>` will give all permissions for all 3 groups ( 4 + 2 + 1 = 7 )
    - Text (too lazy to deal with that rn)


## Running programs

### ./\<program>
- Run program from current directory

### /\<path>/\<program>
- Run program from anywhere

### 2 > /dev/null
- Throws out all error messages returned, can be used on any program