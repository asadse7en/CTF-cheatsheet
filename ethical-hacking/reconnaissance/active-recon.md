# Active Recon

#### Discover active IPs using ARP

```bash
arp-scan $ip/24
```

```bash
netdiscover -r $ip/24
```



### Nmap

```bash
# Scan all ports
nmap -T4 -p- -oN ports.txt $ip

# Version scan and default scripts
nmap -T4 -sC -sV -oN scan.txt $ip
```

<details>

<summary>Cheatsheet</summary>

```bash
#Find hosts alive
nmap -sP $ip/24

#Stealth scan using SYN
nmap -sS $ip

#Stealth scan using FIN
nmap -sF $ip

#Banner Grabbing
nmap -sV -sT $ip

#OS Figerprinting
nmap -O $ip

#Regular Scan
nmap $ip/24

#Enumeration Scan
nmap -p 1-65535 -sV -sS -A -T4 $ip/24

#Output to a file
nmap -oN nmap

#Enumeration Scan All Ports TCP / UDP and output to a txt file
nmap -oN nmap.txt -v -sU -sS -p- -A -T4 $ip

#Quick Scan
nmap -T4 -F $ip/24

#Quick Scan Plus
nmap -sV -T4 -O -F --version-light $ip/24

#Quick Traceroute
nmap -sn --traceroute $ip

#Intense Scan
nmap -T4 -A -v $ip

#Instense Scan Plus UDP
nmap -sS -sU -t4 -A -v $ip/24

#Intense Scan ALL TCP Ports
nmap -p 1-65535 -T4 -A -v $ip/24
Intense Scan - No Ping

#nmap -T4 -A -v -Pn $ip/24
Ping scan
nmap -sn $ip/24

#Slow Comprehensive Scan
nmap -sS -sU -T4 -A -v -PE -PP -PS80,443 -PA3389 -PU40125 -PY -g 53 --script "default or (discovery and safe)" $ip/24

#Run the default scripts and normal port scan against all the found ports
nmap -sC $ip

#Run all nmap scan scripts against found ports
nmap -Pn -sV -O -pT:{TCP ports found},U:{UDP ports found} --script *vuln* $ip

#Port scan with file report
nmap -Pn -sS --stats-every 3m --max-retries 1 --max-scan-delay 20 --defeat-rst-ratelimit -T4 -p1-65535 -oA /root/nmap $ip
```



</details>



