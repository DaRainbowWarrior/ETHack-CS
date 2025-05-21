[Back to Main page](README.md)

# FTP, SSH exploits and using Burpsuite

### FTP exploits
- Depending on the version of FTP found, it's good to look in `msfconsole` or on [Exploit-db](exploit-db.com)
    - RCE is the goal to get into the target machine

### SSH exploits
- To connect without an RSA key `ssh -p <port> username@ip`
    - this does require a password
- To connect whith an RSA key `ssh -p <port> -i <RSA key path> username@ip`
    - On RSA private keys `chmod 600 / 400` is mandatory

### Burpsuite
- A tool used, in this case, mainly to intercept traffic from websites
    - Navigate to `Proxy` -> `Intercept`
    - On the browser set up `FoxyProxy`, only need to set `IP` and `Port`
- To use the internet normally the `Intercept` feature needs to be turned off
- The `Repeater` and `Intruder` tools are the main use for us here
    - Both of them can be used to crack login sites, like Hydra, but with a GUI
    - DON'T try to use `rockyou.txt` with it, it'll freeze the whole attacking machine for a couple minutes


### How to check linux kernel version and distro version
- To check kernel version `uname -a`
- For distribution info, in this case Ubuntu, `cat /etc/lsb-release`
    - These could be used to exploit, but not needed here