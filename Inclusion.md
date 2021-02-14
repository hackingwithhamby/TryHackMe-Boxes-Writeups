TryHackMe.com

box = Inclusion

export IP=10.10.119.169

# NMAP SCANS

```
Starting Nmap 7.91 ( </rich_text>
    <rich_text link="webs https://nmap.org">https://nmap.org</rich_text>
    <rich_text> ) at 2021-01-30 05:20 EST
Nmap scan report for 10.10.119.169 (10.10.119.169)
Host is up (0.37s latency).
Not shown: 998 closed ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 e6:3a:2e:37:2b:35:fb:47:ca:90:30:d2:14:1c:6c:50 (RSA)
|   256 73:1d:17:93:80:31:4f:8a:d5:71:cb:ba:70:63:38:04 (ECDSA)
|_  256 d3:52:31:e8:78:1b:a6:84:db:9b:23:86:f0:1f:31:2a (ED25519)
80/tcp open  http    Werkzeug httpd 0.16.0 (Python 3.6.9)
|_http-server-header: Werkzeug/0.16.0 Python/3.6.9
|_http-title: My blog
No exact OS matches for host (If you know what OS is running on it, see </rich_text>
    <rich_text link="webs https://nmap.org/submit/">https://nmap.org/submit/</rich_text>
    <rich_text> ).
TCP/IP fingerprint:
OS:SCAN(V=7.91%E=4%D=1/30%OT=22%CT=1%CU=44594%PV=Y%DS=4%DC=T%G=Y%TM=6015332
OS:9%P=x86_64-pc-linux-gnu)SEQ(SP=106%GCD=1%ISR=105%TI=Z%CI=Z%II=I%TS=A)SEQ
OS:(SP=106%GCD=1%ISR=105%TI=Z%CI=Z%TS=A)OPS(O1=M505ST11NW6%O2=M505ST11NW6%O
OS:3=M505NNT11NW6%O4=M505ST11NW6%O5=M505ST11NW6%O6=M505ST11)WIN(W1=F4B3%W2=
OS:F4B3%W3=F4B3%W4=F4B3%W5=F4B3%W6=F4B3)ECN(R=Y%DF=Y%T=40%W=F507%O=M505NNSN
OS:W6%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%D
OS:F=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O
OS:=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W
OS:=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=G%R
OS:IPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD=S)

Network Distance: 4 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 21/tcp)
HOP RTT       ADDRESS
1   127.48 ms 10.4.0.1 (10.4.0.1)
2   ... 3
4   383.79 ms 10.10.119.169 (10.10.119.169)

OS and Service detection performed. Please report any incorrect results at </rich_text>
    <rich_text link="webs https://nmap.org/submit/">https://nmap.org/submit/</rich_text>
    <rich_text> .
Nmap done: 1 IP address (1 host up) scanned in 49.09 seconds

```

# USERNAMES AND PASSWORDS
``
falconfeast:rootpassword
``
# INTERESTING FINDS
```
•LFI on /article?name= parameter
• port 22 is open (ssh)
• can use socat as sudo without password
```

# VULNERABILITIES
• Local File Inclusion

# TASKS
```
1. user.txt? = 60989655118397345799
2. root.txt? = 42964104845495153909
```

## PRIVILEGE ESCALATION VECTORS

Method used:
        * by using sudo -l, we can see that we can use socat as root without password.
        * looking at gtfobins:(https://gtfobins.github.io/gtfobins/socat/
      ), we can use the command: (>sudo socat stdin exec:/bin/sh)