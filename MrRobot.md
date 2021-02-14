TryHackMe.com

box = MrRobot

export IP=10.10.36.246

# NMAP SCANS

```
Starting Nmap 7.60 ( https://nmap.org ) at 2021-01-13 10:58 GMT
Nmap scan report for ip-10-10-36-246.eu-west-1.compute.internal (10.10.36.246)
Host is up (0.00040s latency).
Not shown: 997 filtered ports
PORT    STATE  SERVICE  VERSION
22/tcp  closed ssh
80/tcp  open   http     Apache httpd
|_http-server-header: Apache
|_http-title: Site doesn't have a title (text/html).
443/tcp open   ssl/http Apache httpd
|_http-server-header: Apache
|_http-title: Site doesn't have a title (text/html).
| ssl-cert: Subject: commonName=www.example.com
| Not valid before: 2015-09-16T10:45:03
|_Not valid after:  2025-09-13T10:45:03
MAC Address: 02:BE:63:FE:C3:F1 (Unknown)
Aggressive OS guesses: Linux 3.13 (96%), Linux 3.10 - 4.8 (89%), Linux 3.11 (89%), Linux 3.12 (89%), Linux 3.13 or 4.2 (89%), Linux 3.2 - 3.5 (89%), Linux 3.2 - 3.8 (89%), Linux 4.2 (89%), Linux 4.4 (89%), Crestron XPanel control system (88%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 1 hop

TRACEROUTE
HOP RTT     ADDRESS
1   0.40 ms ip-10-10-36-246.eu-west-1.compute.internal (10.10.36.246)

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 30.17 seconds

```

# Usernames and Passwords

```
- elliot (got in fsocity.dic file in robots.txt) | ER28-0652
- robot | abcdefghijklmnopqrstuvwxyz
```

# Interesting Finds

```
- robots.txt has file named fsociety.dic and key-1-of-3.txt
- there is wp-login.php suggesting the webserver is running WordPress.
- gobuster shows there is xmlrpc.php page in the webserver.
- WPScan detected there is /xmlrpc.php that is vulnerable to bruteforce attack.
- we can edit .php theme files(i edited the 404.php file to get a shell, rewrited the 404.php's contents to php-reverse-shell's contents)

```


# Tasks

1. 1st Key?

-found at robots.txt=073403c8a58a1f80d943455fb30724b9

2. 2nd Key?

- found in robot user /home/robot = 822c73956184f694993bede3eb39f959

3. 3rd Key?

-found in /root/root.txt = 04787ddef27c3dee1ee161b21670b4e4

# Notes

* To remove duplicate names in list of usernames or password and output them in different file name:
        command : sort [FILE_NAME] | uniq > [OUTPUT_FILE_NAME]
*

# Privilege Escalation

```
- found weird binary that can run as root (/usr/local/bin/nmap).
- found that we can use this to escalate privileges by looking to gtfobins(https://gtfobins.github.io/gtfobins/nmap/)
- by running : nmap --interactive then typing !sh, we can have a root shell.
