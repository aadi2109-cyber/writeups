
## Introduction
It is an unencrypted remote access service using port **23** and **TCP** connection using the client-server model similar to SSH except it sends the id and password in plain text. 


## Attack Vectors (Methods)

 1.  Packet Sniffing
 2. Credential Harvesting 
 3. Man-in-the-middle (MITM)
 4. Remote Code Execution (RCE)
 5. Banner Grabbing + Reconnaissance
 6. Lateral Movement (in legacy environment)
 7. Backdoor Implantation


## Summary

| **Service**                | Port(s) | Function      | Authentication Types | Vulnerabilities and<br>Misconfiguration                        | Tools for enumeration<br>and exploitation                                              | Uses in cybersecurity                                                                                                                                                                                                                         |
| -------------------------- | ------- | ------------- | -------------------- | -------------------------------------------------------------- | -------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Telecommunication  Network | 23      | Remote Access | unencrypted IAM      | No Encryption(password sent in plain text over TCP connection) | 1. Nmap        2.Wireshark 3. Telnet       4. Netcat      5. Hydra       6. Metasploit | 1.  Packet Sniffing<br> 2. Credential Harvesting <br> 3. Man-in-the-middle (MITM)<br> 4. Remote Code Execution (RCE)<br> 5. Banner Grabbing + Reconnaissance<br> 6. Lateral Movement (in legacy environment)<br> 7. Backdoor Implantation<br> |
|                            |         |               |                      |                                                                |                                                                                        |                                                                                                                                                                                                                                               |

## Quick Notes
