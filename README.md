# Port Scanner

A lightweight TCP port scanner written in pure Python. It checks a list of common ports on a target, names the service that usually runs on each one, and grabs a banner when the service answers.

---

## How it works

For every port in the list, the scanner tries to open a TCP connection with `socket.connect_ex()`:

- `0` means the connection succeeded, so the port is **open** and a service is listening.
- Any other value means the port is **closed** or filtered.

On open web ports (80, 443, 8080) it sends a minimal `GET / HTTP/1.0` request and prints the first line of the reply. Other services, such as SSH, often send a banner on their own, so the scanner just listens for it.

---

## Requirements

- Python 3.7+
- No external libraries, only the standard `socket` and `sys` modules

---

## Usage

```bash
python main.py                  # default target: scanme.nmap.org
python main.py 192.168.1.1      # custom target
```

On Windows you can use `py` instead of `python`.

---

## Sample output

```
Scanning scanme.nmap.org...

[OPEN]  Port    22 — SSH
[OPEN]  Port    80 — HTTP
         Banner: HTTP/1.1 200 OK
[closed] Port   443 — HTTPS
[closed] Port  3306 — MySQL

Scan complete.
```

---

## Ports scanned

| Port | Service  |
| ---- | -------- |
| 21   | FTP      |
| 22   | SSH      |
| 23   | Telnet   |
| 25   | SMTP     |
| 53   | DNS      |
| 80   | HTTP     |
| 110  | POP3     |
| 143  | IMAP     |
| 443  | HTTPS    |
| 3306 | MySQL    |
| 3389 | RDP      |
| 8080 | HTTP-Alt |

---

## Skills demonstrated

- TCP socket programming in Python
- Port scanning and service identification
- Banner grabbing
- Network reconnaissance basics

---

## Roadmap

- [ ] Custom port ranges from the command line (e.g. `1-1024`)
- [ ] Faster scans with threads
- [ ] Proper TLS handshake for banner grabbing on port 443
- [ ] Save results to a file

---

## Credits

Built by Ignat Denis ([@NixDennis](https://github.com/NixDennis)) with help from Bighiu Rares ([@Raresney](https://github.com/Raresney)).

---

## Disclaimer

Use this tool only on systems you own or have explicit permission to scan. Scanning other systems without permission can be illegal.
`scanme.nmap.org` is a host the Nmap project provides specifically for this kind of testing.
