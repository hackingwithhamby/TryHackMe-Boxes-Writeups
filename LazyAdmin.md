TryHackMe.com

Box = LazyAdmin

IP = 10.10.247.101

# NMAP SCANS

```
Starting Nmap 7.60 ( https://nmap.org ) at 2021-01-06 02:07 GMT
Nmap scan report for ip-10-10-247-101.eu-west-1.compute.internal (10.10.247.101)
Host is up (0.0019s latency).
Not shown: 998 closed ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 49:7c:f7:41:10:43:73:da:2c:e6:38:95:86:f8:e0:f0 (RSA)
|   256 2f:d7:c4:4c:e8:1b:5a:90:44:df:c0:63:8c:72:ae:55 (ECDSA)
|_  256 61:84:62:27:c6:c3:29:17:dd:27:45:9e:29:cb:90:5e (EdDSA)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Apache2 Ubuntu Default Page: It works
MAC Address: 02:F6:80:AB:D2:1D (Unknown)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 8.38 seconds

```

# INTERESTING FINDS

```
 - gobuster shows hidden directory: /content/
 - /content/ shows SweetRice CMS installed in web server
 - SweetRice CMS version = 1.5.1 (showed in /content/changelog.txt)
 - SweetRice CMS is vulnerable to  PHP code execution attacks(https://www.exploit-db.com/exploits/40700)
 - can also view backup file in web server(https://www.exploit-db.com/exploits/40718)
 - in the mysql backup file, it shows the hashed password of the webmaster(manager:Password123)
 - /usr/bin/perl can be run as root
 - backup.pl shows .sh file in /etc/copy.sh

```

# ANSWERS
1. user.txt
        - THM{63e5bce9271952aad1113b6f1ac28a07}
2. root.txt
        -THM{6637f41d0177b6f37cb20d775124699f