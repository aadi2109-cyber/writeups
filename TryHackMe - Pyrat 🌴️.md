**Difficulty:** Easy
**Tags:** #Git, #SSH, #Python, #Custom #Socket_Service, #Privilege_Escalation, #Password_Bruteforce

---

***Pyrat receives a curious response from an HTTP server, which leads to a potential Python code execution vulnerability. With a cleverly crafted payload, it is possible to gain a shell on the machine. Delving into the directories, the author uncovers a well-known folder that provides a user with access to credentials. A subsequent exploration yields valuable insights into the application's older version. Exploring possible endpoints using a custom script, the user can discover a special endpoint and ingeniously expand their exploration by fuzzing passwords. The script unveils a password, ultimately granting access to the root.

---

## 🔍 Initial Access (www-data Shell)

* Connected to port `8000` using:

  ```bash
  nc -v 10.10.235.180 8000
  ```
* Got dropped into a shell as user `www-data` without any authentication.
* Confirmed it’s a **custom Python socket server**, not an HTTP service.

---

## 📂 Git Credentials Leak → Lateral Movement

* Explored the server, found a hidden Git repo:

  ```bash
  ls -la /opt/dev/.git
  ```
* Inside the repo, discovered Git logs/configs revealing **GitHub credentials**.
* Used the exposed password to log in via SSH as user `think`:

  ```bash
  ssh think@10.10.235.180
  ```

✅ **User flag retrieved from** `/home/think/user.txt`

---

## 🢨 Privilege Escalation via Backdoored Python Script

* While digging into the Git repo, found an old version of the server:

  ```bash
  git show <commit>
  ```

  or directly:

  ```bash
  cat pyrat.py.old
  ```

* Found a special endpoint in the code:

  ```python
  if data == 'shell':
      shell(client_socket)
  ```

* The `shell()` function spawned a PTY shell, and the server process was confirmed to be running as root:

  ```bash
  ps aux | grep pyrat
  ```

---

## 🔐 Brute-Forcing the Admin Panel (Root Shell)

* The `shell` endpoint required:

  * Sending `admin` once
  * Then bruteforcing the password, with **3 attempts per connection**

* Wrote a script that:

  * Sent `admin`
  * Tried 3 passwords
  * Reconnected on failure
  * Checked for success indicators like `#`, `$`, `root`, `shell`

* Once the correct password was found, the backdoored `/shell` endpoint granted a **root shell**.

✅ **Root flag retrieved from** `/root/root.txt`

---

## 🧠 Summary

| Step    | Description                                           |
| ------- | ----------------------------------------------------- |
| 🔍 1    | Connected to port `8000`, gained `www-data` shell     |
| 🔑 2    | Found GitHub creds in `/opt/dev/.git`                 |
| 🧑‍💻 3 | SSH’d into user `think`                               |
| 🧒 4    | Found backdoored `pyrat.py.old` with `shell` endpoint |
| 💣 5    | Bruteforced `admin` password on `/shell` endpoint     |
| 🧙‍♂️ 6 | Got root shell and captured `root.txt`                |

---

## 😭 Final Thoughts

* Classic CTF-style challenge with real-world flaws:

  * Poor authentication on socket services
  * Git exposure
  * Unvalidated admin backdoors
* Excellent practice for:

  * Socket scripting
  * Git forensics
  * Custom protocol fuzzing
  * Privilege escalation via bad dev hygiene

---

## 🌏 Rooted by: Aadi (aka the Pyrat Slayer)
