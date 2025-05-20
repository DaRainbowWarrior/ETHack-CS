[Back to Main page](README.md)

# Exploiting SUID bits and programs with SUDO permissions

The name of the game here is PE (Permission escalation). Our goal is always to become root\
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