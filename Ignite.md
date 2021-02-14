TryHackMe.com

box = Ignite

export IP=10.10.252.93

# NMAP SCANS

```
Starting Nmap 7.91 ( </rich_text>
    <rich_text link="webs https://nmap.org">https://nmap.org</rich_text>
    <rich_text> ) at 2021-02-11 03:15 EST
Nmap scan report for 10.10.252.93 (10.10.252.93)
Host is up (0.36s latency).
Not shown: 999 closed ports
PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
| http-robots.txt: 1 disallowed entry 
|_/fuel/
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Welcome to FUEL CMS
No exact OS matches for host (If you know what OS is running on it, see </rich_text>
    <rich_text link="webs https://nmap.org/submit/">https://nmap.org/submit/</rich_text>
    <rich_text> ).
TCP/IP fingerprint:
OS:SCAN(V=7.91%E=4%D=2/11%OT=80%CT=1%CU=36664%PV=Y%DS=4%DC=T%G=Y%TM=6024E7E
OS:3%P=x86_64-pc-linux-gnu)SEQ(SP=106%GCD=1%ISR=10A%TI=Z%TS=A)SEQ(SP=106%GC
OS:D=1%ISR=10A%TI=Z%II=I%TS=A)SEQ(SP=106%GCD=1%ISR=10A%TI=Z%CI=I%II=I%TS=A)
OS:OPS(O1=M505ST11NW6%O2=M505ST11NW6%O3=M505NNT11NW6%O4=M505ST11NW6%O5=M505
OS:ST11NW6%O6=M505ST11)WIN(W1=68DF%W2=68DF%W3=68DF%W4=68DF%W5=68DF%W6=68DF)
OS:ECN(R=Y%DF=Y%T=40%W=6903%O=M505NNSNW6%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%
OS:F=AS%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T
OS:5(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=
OS:Z%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF
OS:=N%T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40
OS:%CD=S)

Network Distance: 4 hops

TRACEROUTE (using port 993/tcp)
HOP RTT       ADDRESS
1   124.05 ms 10.4.0.1 (10.4.0.1)
2   ... 3
4   380.82 ms 10.10.252.93 (10.10.252.93)

OS and Service detection performed. Please report any incorrect results at </rich_text>
    <rich_text link="webs https://nmap.org/submit/">https://nmap.org/submit/</rich_text>
    <rich_text> .
Nmap done: 1 IP address (1 host up) scanned in 70.55 seconds

```

# USERNAMES AND PASSWORDS
```
• admin:admin
• root:mememe
```

# INTERESTING FINDS
```
• there is 1 disallowed entry in robots.txt file(/fuel)
• weak credentials used in admin login
• vulnerable to CVE-2018-16763
• by using the above exploit, we can run wget to upload our phpbashshell(https://github.com/Arrexel/phpbash/blob/master/phpbash.php)
```


# TASKS
```
1. user.txt? = 6470e394cbf6dab6a91682cc8585059b
2. root.txt? = b9bbcb33e11b80be759c4e844862482d 		
```

## PRIVILEGE ESCALATION VECTORS
		
Method used:
        * in the /config directory, there is database.php that has the root password
