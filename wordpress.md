[Back to Main page](README.md)

# Wordpress exploitation

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


