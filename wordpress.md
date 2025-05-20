[Back to Main page](README.md)

# Wordpress and Web exploitation

### WPScan
- WPScan is a very important tool, anytime you come across a wordpress site you should use it
- General use command would be `sudo wpscan --url http://<IP adress>`
- it can be used to login into wordpress admin page
    - to use that feature `sudo wpscan --url http://<IP adress> -P <rockyou with path>`
    - WPScan should automatically find users, and try te password file on every one of them
- Otherwise it can list plugins, themes that are vulnerable and can be exploited
- if not found by just `sudo wpscan`, it's located at `/usr/local/bin/wpscan`

### RCE (Remote code execution) using themes
- If you have **access** to the wordpress site's **admin page**, you can use the theme editor to get code running on the target machine
- Navigate to Themes -> Theme editor
    - The code that displays comments is a great choice for RCE
    - Replace the code with the one found in [Chained Reverse shell](crevshell.md) and execute it to get into the target machine
    - Google for `PHP exec example code`

### MSFconsole
- Use this to find exploits for all sorts of stuff
    - Run with `msfconsole`
    - Search with `search <what you want to search for>`
    - To select `select <number of the exploit>`
    - You'll need t fill out some options before running, view them with `options`
    - `set <the option> <what you want to set it to>`
- On some occasions you'll need to set a payload to go with the exploit
    - To see available payloads `show payloads`
    - Set one with `set payload <number>`

### [exploit-db.com](exploit-db.com)
- Helpful place to find exploits on various stuff you discovered
    - Out of date versions of web tools, wordpress stuff, etc.
    - Use the search and be sure to include the version
    - If an exploit is needed from the website, it will be checkmarked

### If a website is located on an internal network
- If a website redirects you to a link which can't be resolved from the outside (aka not using the usual `domain.top-level-domain`)
- You need to know the target pc's IP
    - `sudo nano /etc/hosts` to enter the hosts config on your system
    - After `Others` add this
        - `<Target IP>  <Internal network identifier>`
        - (eg. `40.0.8.15 vtcsec`)
    - Save and exit and try refreshing the site

### A type of PHP exploit
- After completing a form or some other interaction of a website, and the link you see ends in eg. `busque.php?buscar=` it's a vulnerabilty to exploit
    - With `"<your code here>"` put after the `=` there's a good chance you can use RCE on the target machine
    - From there it's easy to use the good ol' [Chained Reverse shell](crevshell.md)





