TryHackMe.com

Box = Blog

export IP=10.10.2.110

# NMAP SCANS

```
# Nmap 7.60 scan initiated Tue Jan 12 11:51:05 2021 as: nmap -A -T4 -oN nmap/NmapScans 10.10.2.110
Nmap scan report for ip-10-10-2-110.eu-west-1.compute.internal (10.10.2.110)
Host is up (0.00045s latency).
Not shown: 996 closed ports
PORT    STATE SERVICE     VERSION
22/tcp  open  ssh         OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 57:8a:da:90:ba:ed:3a:47:0c:05:a3:f7:a8:0a:8d:78 (RSA)
|   256 c2:64:ef:ab:b1:9a:1c:87:58:7c:4b:d5:0f:20:46:26 (ECDSA)
|_  256 5a:f2:62:92:11:8e:ad:8a:9b:23:82:2d:ad:53:bc:16 (EdDSA)
80/tcp  open  http        Apache httpd 2.4.29 ((Ubuntu))
|_http-generator: WordPress 5.0
| http-robots.txt: 1 disallowed entry 
|_/wp-admin/
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: Billy Joel&#039;s IT Blog &#8211; The IT blog
139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp open  netbios-ssn Samba smbd 4.7.6-Ubuntu (workgroup: WORKGROUP)
MAC Address: 02:5B:0A:6C:BA:17 (Unknown)
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.60%E=4%D=1/12%OT=22%CT=1%CU=40803%PV=Y%DS=1%DC=D%G=Y%M=025B0A%T
OS:M=5FFD8D45%P=x86_64-pc-linux-gnu)SEQ(SP=108%GCD=1%ISR=108%TI=Z%CI=Z%TS=A
OS:)SEQ(SP=108%GCD=1%ISR=108%TI=Z%CI=Z%II=I%TS=A)OPS(O1=M2301ST11NW7%O2=M23
OS:01ST11NW7%O3=M2301NNT11NW7%O4=M2301ST11NW7%O5=M2301ST11NW7%O6=M2301ST11)
OS:WIN(W1=F4B3%W2=F4B3%W3=F4B3%W4=F4B3%W5=F4B3%W6=F4B3)ECN(R=Y%DF=Y%T=40%W=
OS:F507%O=M2301NNSNW7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD=0%Q=)T2(R=N
OS:)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=Y%DF=Y%T=40%W=0
OS:%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T7
OS:(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T=40%IPL=164%UN=
OS:0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD=S)

Network Distance: 1 hop
Service Info: Host: BLOG; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_nbstat: NetBIOS name: BLOG, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.7.6-Ubuntu)
|   Computer name: blog
|   NetBIOS computer name: BLOG\x00
|   Domain name: \x00
|   FQDN: blog
|_  System time: 2021-01-12T11:51:32+00:00
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2021-01-12 11:51:32
|_  start_date: 1600-12-31 23:58:45

TRACEROUTE
HOP RTT     ADDRESS
1   0.46 ms ip-10-10-2-110.eu-west-1.compute.internal (10.10.2.110)

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Tue Jan 12 11:51:33 2021 -- 1 IP address (1 host up) scanned in 27.83 seconds

```

# Usernames

```
 - Billy Joel | bjoel
 - Karen Wheeler | kwheel:cutiepie1

```

# Interesting Finds

```
- ports 22,80,139,445 are open (ssh,http,smb)
- gobuster shows /wp-admin that redirects to /wp-login.php
- /rss shows Joel's IT Blog that is available to download
- /rss2 shows Joel's 2nd part of IT Blog
- smb server can be accessed anonymously.
- files in smb server are: (Alice-White-Rabbit.jpg,check-this.png,tswift.mp4)
- .jpg file has password when we try steghide on it.(dont waste time here, no password in the .jpg file and contains text which says: "You've found yourself in a rabbit hole, friend.")
- .png file is a qr code itself.
- WPScan shows the CMS is version 5.0
- WPScan shows /xmlrpc.php 
- /xmlrpc.php responds to POST requests.
- WPScan got the creds for kwheel user.
- The box is vulnerable to CVE-2019-8943.
- Initial foothold: exploited via metasploit module (exploit/multi/http/wp_crop_rce)
```

# TASKS 



1. root.txt

- 9a0b2b618bef9bfa7ac28c1353d9f318

2. user.txt

- c8421899aae571f7af486492b71a8ab7

3. Where was user.txt found?

- /media/usb

4. What CMS was Billy using?

- WordPress

5. What version of the above CMS was being used?

- 5.0

# PRIVILEGE ESCALATION

method used: find / -perm -4000 2>/dev/null

* shows weird binary: /usr/sbin/checker
* using ghidra: we can see that /usr/sbin/checker that it is checking for environment variable `admin` if it is null.
* exploited by setting a value to `admin` variable 

ex: admin=x /usr/sbin/checker