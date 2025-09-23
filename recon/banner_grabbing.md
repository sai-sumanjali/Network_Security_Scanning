# Banner Grabbing 

## 🔍 Purpose
Banner grabbing is used to collect information about services running on open ports, such as software name and version. This helps identify possible vulnerabilities.

---

## 🖥 Methods Used

### 1. Netcat (nc)
```bash
nc -v example.com 80

Sample Output

Connection to example.com 80 port [tcp/http] succeeded!
HTTP/1.1 400 Bad Request
Date: Mon, 22 Sep 2025 12:40:20 GMT
Server: Apache/2.4.41 (Ubuntu)

Tenet

telnet example.com 80

Sample Output

Trying 93.184.216.34...
Connected to example.com.
Escape character is '^]'.
HTTP/1.1 400 Bad Request
Server: Apache/2.4.41 (Ubuntu)
Connection closed by foreign host.

Nmap(Service Detection)

nmap -sV -p 80 example.com

Sample Output

PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))




