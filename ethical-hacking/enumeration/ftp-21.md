# FTP - 21

#### Connect to FTP server

```bash
# Try anonymous login using anonymous:anonymous credentials.

# Using ftp
ftp $ip

# Using netcat
nc $ip 21

# Anonymous FTP dump with Nmap
nmap -v -p 21 --script=ftp-anon.nse $ip
```

#### Vulnerability scan

```
nmap --script=ftp-* -p 21 $ip
```

#### Bruteforcing FTP

```bash
# With hydra
hydra -l user -P /usr/share/john/password.lst ftp://$ip

# With Metasploit
msf> use auxiliary/scanner/ftp/ftp_login
```





