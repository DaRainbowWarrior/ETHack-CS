[Back to Main page](README.md)

# Exploiting SUID bits and programs with SUDO permissions

The name of the game here is PE (Permission escalation). Our goal is always to become root.\
\
Any time we're looking to become root through permission escalation, we need to look for these X main things:

1. ### SUID Bit
- A file with SUID always executes as the user who owns the file, regardless of the user passing the command.
- We can take advantage of this. To look for programs with a SUID bit, use
    - `find / -perm -u=s 2>/dev/null` this will look for any programs with it

2. ### SSH Private keys
- They are usually located at `/home/<username>/.ssh/id-rsa.pub`
- If we find one it can be used, look at [SSH exploits](ftpsshburp.md)

3. ### Do we have sudo permission for anything
- Conduct a search using `sudo -l`
    - **Attention:** it requires the password for the current user

4. ### Any permissions to access `/etc/passwd` or `/etc/shadow` or `/etc/group`
- Access to these, especially `/etc/passwd` or `/etc/shadow` is a great way to get a password for another user account

## Taking advantage of permissions to access `/etc/passwd` or `/etc/shadow`

### getfacl
- Getfacl is a program to view in detail permissions of files and directories
- Simple to use `getfacl <filename>/<directory name>`

### Replacing root password
- In the very little chance the current user we have has a write permission on `/etc/shadow` the root password can be changed to get instant access
- Using a tool like openssl encrypt a new password and replace it with the current root password in `/etc/shadow`
    - `openssl passwd -5 <new password>` this will give the new password hashed
- After that just `su hacker` using the recently hashed password

### Adding a new user with root privileges
- In the slightly better chance the current user we have has a write permission on `/etc/passwd` a new user with root privileges can be added
- A password will need to be hashed with openssl first
- Adding this line into `/etc/passwd` will create the new hacker user
    - eg.  `echo 'hacker:<password hash>:0:0:<any comment>:/root:/bin/bash' >> /etc/passwd`
- After that just `su hacker` using the recently hashed password

### Finding hashed passwords
- Finding a particular entry in `/etc/passwd` is almost a sure way to a password, with some outside program help
    - `username:passwordhash:userid:groupid:comment:homedirectory:shell` this layout
- If permission to view and/or write to `/etc/shadow`
    - `username:passwordhash:blablabla` will be the layout
    - for the password cracking to work, it will be good to transplant the password hash found in `/etc/shadow` (if so is the case) into the layout found in `/etc/passwd`
        - the unknown parts of the layout can be filled with whatever as long as the `username:passwordhash` part is correct

### Cracking hashed passwords with John the Ripper
- After finding or crafting the required little line, save it to a file\
- After navigating to it, the command `sudo john <path+filename>` should be used (UNTESTED)
    - If in the code hash, at the beginning there's a `$y$` instead of `$<number>$`, the command should be modified
    - `sudo john --format=crypt <path+filename>` in this case the correct use