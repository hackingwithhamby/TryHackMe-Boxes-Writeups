TryHackMe.com

box = Relevant

export IP=10.10.35.44

## NMAP SCANS (ALL PORT SCAN)

```
Starting Nmap 7.91 ( </rich_text>
    <rich_text link="webs https://nmap.org">https://nmap.org</rich_text>
    <rich_text> ) at 2021-01-28 05:03 EST
Nmap scan report for 10.10.35.44 (10.10.35.44)
Host is up (0.40s latency).
Not shown: 65527 filtered ports
PORT      STATE SERVICE       VERSION
80/tcp    open  http          Microsoft IIS httpd 10.0
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
|_http-title: IIS Windows Server
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds  Windows Server 2016 Standard Evaluation 14393 microsoft-ds
3389/tcp  open  ms-wbt-server Microsoft Terminal Services
| rdp-ntlm-info: 
|   Target_Name: RELEVANT
|   NetBIOS_Domain_Name: RELEVANT
|   NetBIOS_Computer_Name: RELEVANT
|   DNS_Domain_Name: Relevant
|   DNS_Computer_Name: Relevant
|   Product_Version: 10.0.14393
|_  System_Time: 2021-01-28T10:10:50+00:00
| ssl-cert: Subject: commonName=Relevant
| Not valid before: 2021-01-27T09:56:44
|_Not valid after:  2021-07-29T09:56:44
|_ssl-date: 2021-01-28T10:11:30+00:00; 0s from scanner time.
49663/tcp open  http          Microsoft IIS httpd 10.0
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
|_http-title: IIS Windows Server
49666/tcp open  msrpc         Microsoft Windows RPC
49668/tcp open  msrpc         Microsoft Windows RPC
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running (JUST GUESSING): Microsoft Windows 2016|2012|2008|10 (91%)
OS CPE: cpe:/o:microsoft:windows_server_2016 cpe:/o:microsoft:windows_server_2012 cpe:/o:microsoft:windows_server_2008:r2 cpe:/o:microsoft:windows_10:1607
Aggressive OS guesses: Microsoft Windows Server 2016 (91%), Microsoft Windows Server 2012 (85%), Microsoft Windows Server 2012 or Windows Server 2012 R2 (85%), Microsoft Windows Server 2012 R2 (85%), Microsoft Windows Server 2008 R2 (85%), Microsoft Windows 10 1607 (85%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 4 hops
Service Info: OSs: Windows, Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: mean: 1h36m01s, deviation: 3h34m42s, median: 0s
| smb-os-discovery: 
|   OS: Windows Server 2016 Standard Evaluation 14393 (Windows Server 2016 Standard Evaluation 6.3)
|   Computer name: Relevant
|   NetBIOS computer name: RELEVANT\x00
|   Workgroup: WORKGROUP\x00
|_  System time: 2021-01-28T02:10:52-08:00
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2021-01-28T10:10:53
|_  start_date: 2021-01-28T09:56:45

TRACEROUTE (using port 445/tcp)
HOP RTT       ADDRESS
1   125.31 ms 10.4.0.1 (10.4.0.1)
2   ... 3
4   405.73 ms 10.10.35.44 (10.10.35.44)

OS and Service detection performed. Please report any incorrect results at </rich_text>
    <rich_text link="webs https://nmap.org/submit/">https://nmap.org/submit/</rich_text>
    <rich_text> .
Nmap done: 1 IP address (1 host up) scanned in 493.68 seconds

```

## USERNAMES AND PASSWORDS
```
• Bob - !P@$$W0rD!123
• Bill - Juw4nnaM4n420696969!$$$
```

## INTERESTING FINDS
```
• Default webpage in port 80 stating Microsoft-IIS/10.0 in the http-server-header
• ports 139,445 are open (SMB server), anonymous login allowed
• got credentials in the SMB server(passwords.txt), passwords are base64 encoded
• MSF auxilliary scanner suggested that it might be vulnerable to EternalBlue(MS17-010)
• port 49663 is where the SMB server facing the internet.
• RCE on port 49663 due to anonymous login on SMB.
• SeImpersonatePrivilege is enabled.
```

## VULNERABILITIES
```
• Abuse of SeImpersonate Privilege leads to local privilege escalation.
• CVE-2020-1048 (Windows Print Spooler Vulnerability)
```


## TASKS
```
1. user.txt? = THM{fdk4ka34vk346ksxfr21tg789ktf45}
2. root.txt? = THM{1fk5kf469devly1gl320zafgl345pv}
```

## PRIVILEGE ESCALATION VECTORS
```
Methods used:
    * SeImpersonatePrivilege is enabled in the machine that can be used for local privilege escalation
    * by using printspoofer.exe we managed to be as NT AUTHORITY \SYSTEM
```