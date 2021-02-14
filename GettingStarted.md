TryHackMe.com

box = Getting Started

export IP=10.10.177.221

# NMAP SCANS

```
Starting Nmap 7.91 (https://nmap.org) at 2021-02-07 06:57 EST
Nmap scan report for 10.10.177.221 (10.10.177.221)
Host is up (0.38s latency).
Not shown: 997 closed ports
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.1 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 72:b4:14:14:87:9d:4a:86:df:44:25:16:e8:0c:74:32 (RSA)
|   256 55:5b:d2:b8:fe:8b:88:f5:7d:47:18:4c:fb:d8:97:5b (ECDSA)
|_  256 4c:ab:b1:f3:c6:6e:00:39:98:5b:b1:13:17:ef:49:d1 (ED25519)
80/tcp   open  http    Node.js (Express middleware)
|_http-title: BFFs
3000/tcp open  http    Node.js (Express middleware)
|_http-title: BFFs
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/.
TCP/IP fingerprint:
OS:SCAN(V=7.91%E=4%D=2/7%OT=22%CT=1%CU=34893%PV=Y%DS=4%DC=T%G=Y%TM=601FD5CB
OS:%P=x86_64-pc-linux-gnu)SEQ(SP=105%GCD=1%ISR=10B%TI=Z%CI=Z%II=I%TS=A)OPS(
OS:O1=M505ST11NW7%O2=M505ST11NW7%O3=M505NNT11NW7%O4=M505ST11NW7%O5=M505ST11
OS:NW7%O6=M505ST11)WIN(W1=F4B3%W2=F4B3%W3=F4B3%W4=F4B3%W5=F4B3%W6=F4B3)ECN(
OS:R=Y%DF=Y%T=40%W=F507%O=M505NNSNW7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS
OS:%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=
OS:Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=
OS:R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T
OS:=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD=
OS:S)

Network Distance: 4 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 554/tcp)
HOP RTT       ADDRESS
1   123.57 ms 10.4.0.1 (10.4.0.1)
2   ... 3
4   380.48 ms 10.10.177.221 (10.10.177.221)

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/.
Nmap done: 1 IP address (1 host up) scanned in 52.09 seconds

```


# USERNAMES AND PASSWORDS
```
• admin:admin (admin page)
```

# INTERESTING FINDS
```
• Web server is running Node.js
• /test-admin is a admin page (found by viewing page source)
• using weak credentials


# TASKS

1. Name of the hidden admin page? = /test-admin
2. Username and password in the form? = admin:admin
3. How many users in the application? = 3
```