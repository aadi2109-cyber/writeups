### Introduction

It is a windows service used for sharing files, printers and disk .
It is a Request-Response protocol using TCP port 445 in modern version and NETBIOS over TCP/IP in older models
### Importance in Cybersecurity

1. Misconfiguration in shares (no auth / weak permissions)
2. Exposed credentials or sensitive files
3. Hidden backups of databases, password files, config files
4. NTLM hashes
5. Pass-the-Hash
6. NTLM relay (impersonate users)
7. Brute-force attacks on SMB logins
8. Pivoting

### Summary

| **Service**                          | Port(s)                                | Function                                                                | Authentication Types                                                                                                                                                   | Vulnerabilities and<br>Misconfiguration                                                                                                                                                                                                                                                                                                                                                                                                 | Tools for enumeration<br>and exploitation                                                                                                                  | Uses in cybersecurity                                                                                                                                                                                                                                                                             |
| ------------------------------------ | -------------------------------------- | ----------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Server Message Block<br><br>Protocol | 445 (139-137 in older NetBios version) | To share network services like Printer devices, disk, serial ports, etc | 1. NTLM in older version (weak)<br>    <br>2. Kerberos (New and efficient . Used in AD environment.)<br>    <br>3. Anonymous login (worst type. Has no Authentication) | 1. SMBv1 has a RCE [CVE-2017-7494](https://www.cvedetails.com/cve/CVE-2017-7494/)<br>    <br>2. Misconfiguration in shares (no auth / weak permissions)<br>    <br>3. Exposed credentials or sensitive files<br>    <br>4. Hidden backups of databases, password files, config files<br>    <br>5. NTLM hashes<br>    <br>6. Pass-the-Hash<br>    <br>7. NTLM relay (impersonate users)<br>    <br>8. Brute-force attacks on SMB logins | 1. Enum4linux<br>    <br>2. Nmap<br>    <br>3. Smbclient<br>    <br>4. Respoder<br>    <br>5. Impacket<br>    <br>6. CrackMapExec<br>    <br>7. Metasploit | 1. Can be used to get foothold access of a target network<br>    <br>2. Used to pivot between devices and networks<br>    <br>3. gain access to sensitive files like ids passwords and hashes<br>    <br>4. used in Active Directory so it can be used to compromise domain controller also (KDC) |

### Quick Notes