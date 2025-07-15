
## Introduction

File Transfer Protocol is used to transfer files using TCP connection between two devices using port 21 (and 20 for sending data in active mode). 
It uses two modes to transfer files :-
- ### Active
- ### Passive

In Active mode the client controls the connection and defines the port to the server to send the data back to the client from server's port 20 (kinda of reverse connection causing problems for firewall) . 

In Passive mode the server defines a higher port for data connection 
which the client connects through firewall . 

## Attack Vectors (Methods)

1. Anonymous Login abuse 
2. Brute-force login
3. sniffing credentials
4. File Uploads + RCE
5. Directory Traversal
6. Exploiting known vulnerablities
7. Banner grabbing
8. FTP bounce attack 
9. Malware Hosting


## Summary

| **Service**        | Port(s)                      | Function                                                | Authentication Types                                 | Vulnerabilities and<br>Misconfiguration                                                                                                                                                                                                                                                                                                                                                      | Tools for enumeration<br>and exploitation                                                                                                                                                                                                      | Uses in cybersecurity |
| ------------------ | ---------------------------- | ------------------------------------------------------- | ---------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------- |
| File Transfer Port | 21 (21-20 for active method) | transferring files between devices using TCP connection | unencrypted and sometimes allows anonymous FTP login | 1. RCE in vsftpd   v2.3.4 [CVE-2011-2523](ttps://nvd.nist.gov/vuln/detail/CVE-2011-2523)                                      2. Anonymous login allowed in most systems                                  3. Passwords and ID send over TCP connect 1. Nmap        2.Wireshark 3. Netcat      4.msfconsole  5. hydra        6.searchsploit 7.PHP (For web shells)  .  .  .  .  .  .  .  .  . | 1. Anonymous Login abuse <br>2. Brute-force login<br>3. sniffing credentials<br>4. File Uploads + RCE<br>5. Directory Traversal<br>6. Exploiting known vulnerablities<br>7. Banner grabbing<br>8. FTP bounce attack <br>9. Malware Hosting<br> |                       |

#review 
## Quick Notes
