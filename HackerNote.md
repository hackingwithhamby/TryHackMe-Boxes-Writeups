TryHackMe.com

export IP = 10.10.72.219

## NMAP SCANS

```
Starting Nmap 7.91 ( https://nmap.org ) at 2021-02-14 03:27 PST
Nmap scan report for 10.10.72.219 (10.10.72.219)
Host is up (0.40s latency).
Not shown: 997 closed ports
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 10:a6:95:34:62:b0:56:2a:38:15:77:58:f4:f3:6c:ac (RSA)
|   256 6f:18:27:a4:e7:21:9d:4e:6d:55:b3:ac:c5:2d:d5:d3 (ECDSA)
|_  256 2d:c3:1b:58:4d:c3:5d:8e:6a:f6:37:9d:ca:ad:20:7c (ED25519)
80/tcp   open  http    Golang net/http server (Go-IPFS json-rpc or InfluxDB API)
|_http-title: Home - hackerNote
8080/tcp open  http    Golang net/http server (Go-IPFS json-rpc or InfluxDB API)
|_http-open-proxy: Proxy might be redirecting requests
|_http-title: Home - hackerNote
Aggressive OS guesses: Linux 3.1 (95%), Linux 3.2 (95%), AXIS 210A or 211 Network Camera (Linux 2.6.17) (94%), ASUS RT-N56U WAP (Linux 3.4) (93%), Linux 3.16 (93%), Linux 2.6.32 (92%), Linux 2.6.39 - 3.2 (92%), Linux 3.1 - 3.2 (92%), Linux 3.11 (92%), Linux 3.2 - 4.9 (92%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 4 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 256/tcp)
HOP RTT       ADDRESS
1   144.00 ms 10.4.0.1 (10.4.0.1)
2   ... 3
4   400.55 ms 10.10.72.219 (10.10.72.219)

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 55.45 seconds

```

## USERNAMES AND PASSWORDS

```
WEB -> james:blue7
SSH -> james:dak4ddb37b
```

## INTERESTING FINDS

```
* Login form is vulnerable to timing exploit
* james user has SSH creds in webpage.
* Machine is vulnerable to CVE-2019-18634
```

## TASKS

```
1. Which ports are open? (in numerical order) = 22,80,8080
2. What programming language is the backend written in? = go
3. How many usernames from the list are valid? = 1
4. What are/is the valid username(s)? = james
5. How many passwords were in your wordlist? = 180
6. What was the user's password? = blue7
7. What's the user's SSH password? = dak4ddb37b
8. User flag? = thm{56911bd7ba1371a3221478aa5c094d68}
9. CVE number of the exploit? = CVE-2019-18634
10. Root.txt? = thm{af55ada6c2445446eb0606b5a2d3a4d2}
```

### PRIVILEGE ESCALATION VECTORS

Method Used:

1. CVE-2019-18634 = sudo 'pwdfeedback' exploit leads to local privilege escalation.
2. by using this github repo: (https://github.com/saleemrashid/sudo-cve-2019-18634), we use the POC to exploit the system. This CVE exploits the pwdfeedback option in inputting password.
