
## Introduction

Network File System or NFS is a remote file system for local networks using TCP port 2049 . It uses a client-server protocol that allows directories and files with others over a network . 
### Working 
NFS server exports the directory using the /etc/exports file . It then waits for client to connect to port 2049 and then establishes connection using portmap or rcpbind .
NFS client searches for the available directories using showmount command and then requests the directory to be mounted and then can read/write as if it were its own filesystem . 

## Vulnerablities Attack Vectors (Methods)

1. No encryption -- MITM attacks
2. IP based Authentication (IPV4) -- Spoofing attacks
3. UID/GID based permissions -- Spoofing and Privesc
4. No_root_squash -- Privesc

## Summary


| **Service**         | Port(s) | Function            | Authentication Types                                           | Vulnerabilities and<br>Misconfiguration                                                                                                                                               | Tools for enumeration<br>and exploitation | Uses in cybersecurity                                                                                     |
| ------------------- | ------- | ------------------- | -------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| Network File System | 2049    | Sharing Filesystems | No encryption   IPV4 based auhentication   local UID/GID based | <br>1. No encryption -- MITM attacks<br>2. IP based Authentication (IPV4) -- Spoofing attacks<br>3. UID/GID based permissions -- Spoofing and Privesc<br>4. No_root_squash -- Privesc |                                           | 1. Foothold access            2.Privesc        3. Pivoting      4.Information Disclosure        2.Privesc |

## Quick Notes