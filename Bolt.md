TryHackMe.com

box = Bolt

export IP=10.10.15.11

# NMAP SCANS

```
Starting Nmap 7.91 (https://nmap.org) at 2021-01-30 05:39 EST
Nmap scan report for 10.10.15.11 (10.10.15.11)
Host is up (0.36s latency).
Not shown: 997 closed ports
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 f3:85:ec:54:f2:01:b1:94:40:de:42:e8:21:97:20:80 (RSA)
|   256 77:c7:c1:ae:31:41:21:e4:93:0e:9a:dd:0b:29:e1:ff (ECDSA)
|_  256 07:05:43:46:9d:b2:3e:f0:4d:69:67:e4:91:d3:d3:7f (ED25519)
80/tcp   open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: Apache2 Ubuntu Default Page: It works
8000/tcp open  http    (PHP 7.2.32-1)
| fingerprint-strings: 
|   FourOhFourRequest: 
|     HTTP/1.0 404 Not Found
|     Date: Sat, 30 Jan 2021 10:39:27 GMT
|     Connection: close
|     X-Powered-By: PHP/7.2.32-1+ubuntu18.04.1+deb.sury.org+1
|     Cache-Control: private, must-revalidate
|     Date: Sat, 30 Jan 2021 10:39:27 GMT
|     Content-Type: text/html; charset=UTF-8
|     pragma: no-cache
|     expires: -1
|     X-Debug-Token: a3f218
|     &lt;!doctype html&gt;
|     &lt;html lang="en"&gt;
|     &lt;head&gt;
|     &lt;meta charset="utf-8"&gt;
|     &lt;meta name="viewport" content="width=device-width, initial-scale=1.0"&gt;
|     &lt;title&gt;Bolt | A hero is unleashed&lt;/title&gt;
|     &lt;link href="</rich_text>
    <rich_text link="webs https://fonts.googleapis.com/css?family=Bitter|Roboto:400,400i,700&quot;">https://fonts.googleapis.com/css?family=Bitter|Roboto:400,400i,700"</rich_text>
    <rich_text> rel="stylesheet"&gt;
|     &lt;link rel="stylesheet" href="/theme/base-2018/css/bulma.css?8ca0842ebb"&gt;
|     &lt;link rel="stylesheet" href="/theme/base-2018/css/theme.css?6cb66bfe9f"&gt;
|     &lt;meta name="generator" content="Bolt"&gt;
|     &lt;/head&gt;
|     &lt;body&gt;
|     href="#main-content" class="vis
|   GetRequest: 
|     HTTP/1.0 200 OK
|     Date: Sat, 30 Jan 2021 10:39:26 GMT
|     Connection: close
|     X-Powered-By: PHP/7.2.32-1+ubuntu18.04.1+deb.sury.org+1
|     Cache-Control: public, s-maxage=600
|     Date: Sat, 30 Jan 2021 10:39:26 GMT
|     Content-Type: text/html; charset=UTF-8
|     X-Debug-Token: 454b3b
|     &lt;!doctype html&gt;
|     &lt;html lang="en-GB"&gt;
|     &lt;head&gt;
|     &lt;meta charset="utf-8"&gt;
|     &lt;meta name="viewport" content="width=device-width, initial-scale=1.0"&gt;
|     &lt;title&gt;Bolt | A hero is unleashed&lt;/title&gt;
|     &lt;link href="</rich_text>
    <rich_text link="webs https://fonts.googleapis.com/css?family=Bitter|Roboto:400,400i,700&quot;">https://fonts.googleapis.com/css?family=Bitter|Roboto:400,400i,700"</rich_text>
    <rich_text> rel="stylesheet"&gt;
|     &lt;link rel="stylesheet" href="/theme/base-2018/css/bulma.css?8ca0842ebb"&gt;
|     &lt;link rel="stylesheet" href="/theme/base-2018/css/theme.css?6cb66bfe9f"&gt;
|     &lt;meta name="generator" content="Bolt"&gt;
|     &lt;link rel="canonical" href="</rich_text>
    <rich_text link="webs http://0.0.0.0:8000/&quot;&gt;">http://0.0.0.0:8000/"&gt;</rich_text>
    <rich_text>
|     &lt;/head&gt;
|_    &lt;body class="front"&gt;
|_http-generator: Bolt
|_http-title: Bolt | A hero is unleashed
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at </rich_text>
    <rich_text link="webs https://nmap.org/cgi-bin/submit.cgi?new-service">https://nmap.org/cgi-bin/submit.cgi?new-service</rich_text>
    <rich_text> :
SF-Port8000-TCP:V=7.91%I=7%D=1/30%Time=6015375E%P=x86_64-pc-linux-gnu%r(Ge
SF:tRequest,29E1,"HTTP/1\.0\x20200\x20OK\r\nDate:\x20Sat,\x2030\x20Jan\x20
SF:2021\x2010:39:26\x20GMT\r\nConnection:\x20close\r\nX-Powered-By:\x20PHP
SF:/7\.2\.32-1\+ubuntu18\.04\.1\+deb\.sury\.org\+1\r\nCache-Control:\x20pu
SF:blic,\x20s-maxage=600\r\nDate:\x20Sat,\x2030\x20Jan\x202021\x2010:39:26
SF:\x20GMT\r\nContent-Type:\x20text/html;\x20charset=UTF-8\r\nX-Debug-Toke
SF:n:\x20454b3b\r\n\r\n&lt;!doctype\x20html&gt;\n&lt;html\x20lang=\"en-GB\"&gt;\n\x20\
SF:x20\x20\x20&lt;head&gt;\n\x20\x20\x20\x20\x20\x20\x20\x20&lt;meta\x20charset=\"u
SF:tf-8\"&gt;\n\x20\x20\x20\x20\x20\x20\x20\x20&lt;meta\x20name=\"viewport\"\x20
SF:content=\"width=device-width,\x20initial-scale=1\.0\"&gt;\n\x20\x20\x20\x2
SF:0\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20&lt;title&gt;Bolt\x20\|\x20A
SF:\x20hero\x20is\x20unleashed&lt;/title&gt;\n\x20\x20\x20\x20\x20\x20\x20\x20&lt;l
SF:ink\x20href=\"</rich_text>
    <rich_text link="webs https://fonts\.googleapis\.com/css\?family=Bitter\|Roboto">https://fonts\.googleapis\.com/css\?family=Bitter\|Roboto</rich_text>
    <rich_text>
SF::400,400i,700\"\x20rel=\"stylesheet\"&gt;\n\x20\x20\x20\x20\x20\x20\x20\x2
SF:0&lt;link\x20rel=\"stylesheet\"\x20href=\"/theme/base-2018/css/bulma\.css\
SF:?8ca0842ebb\"&gt;\n\x20\x20\x20\x20\x20\x20\x20\x20&lt;link\x20rel=\"styleshe
SF:et\"\x20href=\"/theme/base-2018/css/theme\.css\?6cb66bfe9f\"&gt;\n\x20\x20
SF:\x20\x20\t&lt;meta\x20name=\"generator\"\x20content=\"Bolt\"&gt;\n\x20\x20\x2
SF:0\x20\t&lt;link\x20rel=\"canonical\"\x20href=\"</rich_text>
    <rich_text link="webs http://0\.0\.0\.0:8000/\&quot;&gt;\">http://0\.0\.0\.0:8000/\"&gt;\</rich_text>
    <rich_text>
SF:n\x20\x20\x20\x20&lt;/head&gt;\n\x20\x20\x20\x20&lt;body\x20class=\"front\"&gt;\n\x
SF:20\x20\x20\x20\x20\x20\x20\x20&lt;a\x20")%r(FourOhFourRequest,16C3,"HTTP/1
SF:\.0\x20404\x20Not\x20Found\r\nDate:\x20Sat,\x2030\x20Jan\x202021\x2010:
SF:39:27\x20GMT\r\nConnection:\x20close\r\nX-Powered-By:\x20PHP/7\.2\.32-1
SF:\+ubuntu18\.04\.1\+deb\.sury\.org\+1\r\nCache-Control:\x20private,\x20m
SF:ust-revalidate\r\nDate:\x20Sat,\x2030\x20Jan\x202021\x2010:39:27\x20GMT
SF:\r\nContent-Type:\x20text/html;\x20charset=UTF-8\r\npragma:\x20no-cache
SF:\r\nexpires:\x20-1\r\nX-Debug-Token:\x20a3f218\r\n\r\n&lt;!doctype\x20html
SF:&gt;\n&lt;html\x20lang=\"en\"&gt;\n\x20\x20\x20\x20&lt;head&gt;\n\x20\x20\x20\x20\x20\
SF:x20\x20\x20&lt;meta\x20charset=\"utf-8\"&gt;\n\x20\x20\x20\x20\x20\x20\x20\x2
SF:0&lt;meta\x20name=\"viewport\"\x20content=\"width=device-width,\x20initial
SF:-scale=1\.0\"&gt;\n\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x2
SF:0\x20\x20&lt;title&gt;Bolt\x20\|\x20A\x20hero\x20is\x20unleashed&lt;/title&gt;\n\x2
SF:0\x20\x20\x20\x20\x20\x20\x20&lt;link\x20href=\"</rich_text>
    <rich_text link="webs https://fonts\.googleapis\">https://fonts\.googleapis\</rich_text>
    <rich_text>
SF:.com/css\?family=Bitter\|Roboto:400,400i,700\"\x20rel=\"stylesheet\"&gt;\n
SF:\x20\x20\x20\x20\x20\x20\x20\x20&lt;link\x20rel=\"stylesheet\"\x20href=\"/
SF:theme/base-2018/css/bulma\.css\?8ca0842ebb\"&gt;\n\x20\x20\x20\x20\x20\x20
SF:\x20\x20&lt;link\x20rel=\"stylesheet\"\x20href=\"/theme/base-2018/css/them
SF:e\.css\?6cb66bfe9f\"&gt;\n\x20\x20\x20\x20\t&lt;meta\x20name=\"generator\"\x2
SF:0content=\"Bolt\"&gt;\n\x20\x20\x20\x20&lt;/head&gt;\n\x20\x20\x20\x20&lt;body&gt;\n\x
SF:20\x20\x20\x20\x20\x20\x20\x20&lt;a\x20href=\"#main-content\"\x20class=\"v
SF:is");
Aggressive OS guesses: Linux 3.1 (95%), Linux 3.2 (95%), AXIS 210A or 211 Network Camera (Linux 2.6.17) (94%), ASUS RT-N56U WAP (Linux 3.4) (93%), Linux 3.16 (93%), Linux 2.6.32 (92%), Linux 2.6.39 - 3.2 (92%), Linux 3.1 - 3.2 (92%), Linux 3.2 - 4.9 (92%), Linux 3.7 - 3.10 (92%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 4 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 80/tcp)
HOP RTT       ADDRESS
1   123.74 ms 10.4.0.1 (10.4.0.1)
2   ... 3
4   380.53 ms 10.10.15.11 (10.10.15.11)

OS and Service detection performed. Please report any incorrect results at </rich_text>
    <rich_text link="webs https://nmap.org/submit/">https://nmap.org/submit/</rich_text>
    <rich_text> .
Nmap done: 1 IP address (1 host up) scanned in 74.37 seconds

```

# USERNAMES AND PASSWORDS
```
• bolt:boltadmin123
```

# INTERESTING FINDS
```
• CMS is running on port 8000
• Bolt CMS is running.
• CMS version is Bolt 3.7.1
```

# VULNERABILITIES
```
• Bolt CMS 3.7.x is vulnerable to authenticated remote code execution
```

# TASKS
```
1. CMS is running on port? = 8000
2. Username found in CMS? = bolt
3. Password for the username? = boltadmin123
4. CMS version? = Bolt 3.7.1
5. EDB-ID(Exploit-DB ID)? = 48296
6. Exploit module that can be used? = unix/webapp/bolt_authenticated_rce
7. flag.txt? = THM{wh0_d035nt_l0ve5_b0l7_r1gh7?}
```

## PRIVILEGE ESCALATION VECTORS
Methods Used:
        * Metasploit module exploit/unix/webapp/bolt_authenticated_rce gives us root shell after giving correct credentials.