## Protocol Overview

Simple Mail Transfer Protocol - SMTP is a client-server protocol which sends email to the server . The service can only send mails but can't recieve it. 
## Ports Used

```
25 -- Server to Server connection (blocked due to spam)
587 -- Client to Server connection (used in modern systems)
465 -- SMTP over SSL (Legacy but used in some systems)
```

## How It Works

1. CONNECTON INITIATION 
```
EHLO or HELO
```
 
 2.  DEFINE SENDER
 ```
 MAIL FROM :
```

3. DEFINE RECIPIENT
```
RCPT TO :
```

4. WRITING MESSAGE
```
DATA
```

5. ENDING MESSAGE
```
. 
```

6. CLOSING THE SESSION 
```
QUIT
```
## Attack Vectors

1. Email spoofing (Phishing)
2. Open Relay (spam)
3. MITM attacks 
4. User enumeration (VRFY/RCPT TO)
5. 

## Tools + Commands
## Real Exploits
## Summary Table

| **Service** | Port(s) | Function | Authentication Types | Vulnerabilities and<br>Misconfiguration | Tools for enumeration<br>and exploitation | Uses in cybersecurity |
| ----------- | ------- | -------- | -------------------- | --------------------------------------- | ----------------------------------------- | --------------------- |
## Quick Notes
