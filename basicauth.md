[Back to Main page](README.md)

# Basic Authentication

The basics of finding and getting into a target.

### ping \<IP adress> / \<Link>
- Pings the target, confirming if it's online or not.

## Scanning the target

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


