TryHackMe.com

box=Anonymous

export IP=10.10.66.138

# NMAP SCANS

```
Starting Nmap 7.91 (https://nmap.org) at 2021-02-04 05:49 EST
Nmap scan report for 10.10.66.138 (10.10.66.138)
Host is up (0.38s latency).
Not shown: 996 closed ports
PORT    STATE SERVICE     VERSION
21/tcp  open  ftp         vsftpd 2.0.8 or later
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_drwxrwxrwx    2 111      113          4096 Jun 04  2020 scripts [NSE: writeable]
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:10.4.21.189
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 4
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
22/tcp  open  ssh         OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 8b:ca:21:62:1c:2b:23:fa:6b:c6:1f:a8:13:fe:1c:68 (RSA)
|   256 95:89:a4:12:e2:e6:ab:90:5d:45:19:ff:41:5f:74:ce (ECDSA)
|_  256 e1:2a:96:a4:ea:8f:68:8f:cc:74:b8:f0:28:72:70:cd (ED25519)
139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp open  netbios-ssn Samba smbd 4.7.6-Ubuntu (workgroup: WORKGROUP)
No exact OS matches for host (If you know what OS is running on it, see </rich_text>
    <rich_text link="webs https://nmap.org/submit/">https://nmap.org/submit/</rich_text>
    <rich_text> ).
TCP/IP fingerprint:
OS:SCAN(V=7.91%E=4%D=2/4%OT=21%CT=1%CU=37607%PV=Y%DS=4%DC=T%G=Y%TM=601BD186
OS:%P=x86_64-pc-linux-gnu)SEQ(SP=102%GCD=1%ISR=106%TI=Z%CI=Z%II=I%TS=A)SEQ(
OS:SP=102%GCD=1%ISR=106%TI=Z%CI=Z%TS=A)OPS(O1=M505ST11NW6%O2=M505ST11NW6%O3
OS:=M505NNT11NW6%O4=M505ST11NW6%O5=M505ST11NW6%O6=M505ST11)WIN(W1=F4B3%W2=F
OS:4B3%W3=F4B3%W4=F4B3%W5=F4B3%W6=F4B3)ECN(R=Y%DF=Y%T=40%W=F507%O=M505NNSNW
OS:6%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF
OS:=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=
OS:%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=
OS:0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=G%RI
OS:PCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD=S)

Network Distance: 4 hops
Service Info: Host: ANONYMOUS; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_clock-skew: mean: 0s, deviation: 1s, median: 0s
|_nbstat: NetBIOS name: ANONYMOUS, NetBIOS user: &lt;unknown&gt;, NetBIOS MAC: &lt;unknown&gt; (unknown)
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.7.6-Ubuntu)
|   Computer name: anonymous
|   NetBIOS computer name: ANONYMOUS\x00
|   Domain name: \x00
|   FQDN: anonymous
|_  System time: 2021-02-04T10:50:34+00:00
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2021-02-04T10:50:34
|_  start_date: N/A

TRACEROUTE (using port 1025/tcp)
HOP RTT       ADDRESS
1   126.71 ms 10.4.0.1 (10.4.0.1)
2   ... 3
4   382.79 ms 10.10.66.138 (10.10.66.138)

OS and Service detection performed. Please report any incorrect results at </rich_text>
    <rich_text link="webs https://nmap.org/submit/">https://nmap.org/submit/</rich_text>
    <rich_text> .
Nmap done: 1 IP address (1 host up) scanned in 58.70 seconds

```

# USERNAMES AND PASSWORDS
• namelessone: N/A


# INTERESTING FINDS
```
• FTP and SMB service can be logon as anonymous.
• port 22 is open
• corgo2.jpg and puppos.jpeg has passwords
• writeable .sh file and ftp service
• user namelessone is part of lxc group
```

# TASKS
```
1. How many ports are open? = 4
2. service running on port 21? = ftp 
3. service running on port 139,445? = smb
4. User's share? = pics
5. user.txt? = 90d6f992585815ff991e68748c414740
6. root.txt? = 4d930091c31a622a7ed10f27999af363
```

## PRIVILEGE ESCALATION VECTORS	

Method Used:
   1. user namelessone is part of lxc group which is a container.
   2. we can use (https://book.hacktricks.xyz/linux-unix/privilege-escalation/interesting-groups-linux-pe/lxd-privilege-escalation)
   3. in summary, we can create a privileged container and we can escalate to root and can navigate to directory where root user can only access.
    
