# LoFi -- (TryHackMe)

--- 
## IP - 10.10.85.95/10.10.4.37
---  
## Nmap results :- 

Starting Nmap 7.95 ( https://nmap.org ) at 2025-07-02 15:28 IST
Nmap scan report for 10.10.85.95
Host is up (0.23s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 3e:51:bf:86:0b:fc:e9:9a:59:7d:92:c3:71:da:cb:73 (RSA)
|   256 cc:02:aa:16:63:a2:03:b6:da:21:73:48:a3:e0:08:c8 (ECDSA)
|_  256 6a:11:b7:0d:df:a5:19:ce:51:e6:ed:cf:24:90:76:96 (ED25519)
80/tcp open  http    Apache httpd 2.2.22 ((Ubuntu))
|_http-title: Lo-Fi Music
|_http-server-header: Apache/2.2.22 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 23.14 seconds


## LoFi site at port 80

![[Screenshot_2025-07-02_22_20_28.png]]

## attempt for RCE 

![[Screenshot_2025-07-02_19_25_53.png]]
(failed as the path is blacklisted)


## flag found 

![[Screenshot_2025-07-02_22_22_04.png]]

JUST FIND OUT THE FLAG LOCATION !!!!!