# Snort Challenge - The Basics

**Room Link:** [https://tryhackme.com/room/snortchallenges1](https://tryhackme.com/room/snortchallenges1)





## Writing IDS Rules (HTTP)

\
**Navigate to the task folder.**\
**Use the given pcap file.**\
**Write rules to detect "all TCP port 80 traffic" packets in the given pcap file.**&#x20;

**What is the number of detected packets?**

**local.rules**

```
alert tcp any any <> any 80 (msg:"TCP Port 80 Traffic Detected inbound"; sid:10001;)
alert tcp any 80 <> any any (msg:"TCP Port 80 Traffic Detected outbound"; sid:10002;)
```

**Kali**

```
sudo snort -c local.rules -r mx-3.pcap -A full -l .
```

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

**What is the destination address of packet 63?**

The easiest way to look at a certain packet is to use -n to only show the amount of packets we want to see.

**Kali**

```
sudo snort -r snort.log.1690286170 -n63
```

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

**What is the ACK number of packet 64?**

**Kali**

```
sudo snort -r snort.log.1690286170 -n64
```

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

**What is the SEQ number of packet 62?**

**Kali**

```
sudo snort -r snort.log.1690286170 -n62
```

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

**What is the TTL of packet 65?**

**Kali**

```
sudo snort -r snort.log.1690286170 -n65
```

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

**What is the source IP of packet 65?**

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

**What is the source port of packet 65?**

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>



## Writing IDS Rules (FTP)

**local.rules**

```
alert tcp any any <> any 21 (msg:"FTP inbound"; sid:10001;)
alert tcp any 21 <> any any (msg:"FTP outbound"; sid:10002;)
```

**What is the number of detected packets?**

**Kali**

```
sudo snort -c local.rules -r ftp-png-gif.pcap -A full -l .
```

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

**What is the FTP service name?**

**Kali**

```
sudo snort -r snort.log.1690287034 -X
```

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

**Write a rule to detect failed FTP login attempts in the given pcap. What is the FTP service name?**

**local.rules**

```
alert tcp any any <> any 21 (msg: "Failed FTP Login"; content:"530 User"; sid: 100003; rev: 1;)alert tcp any any <> any 21 (msg: "Failed FTP Login"; content:"530 User"; sid: 100003; rev: 1;)alert tcp any any <> any 21 (msg: "Failed FTP Login"; content:"530 User"; sid: 100003; rev: 1;)
```

**Kali**

```
sudo snort -c local.rules -r ftp-png-gif.pcap -A full -l .
```

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>



**Write a rule to detect successful FTP logins in the given pcap. What is the number of detected packets?**

**local.rules**

```
alert TCP any any <> any 21 (msg:"FTP Success Login"; content:"230 User"; sid:100000; rev:1;)
```

**Kali**

```
sudo snort -c local.rules -r ftp-png-gif.pcap -A full -l .
```

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

**Write a rule to detect failed FTP login attempts with a valid username but a bad password or no password. What is the number of detected packets?**

**local.rules**

```
alert tcp any any <> any 21 (msg: "FTP Failed Login-Bad or No Password"; content:"331 Password"; sid: 100005; rev: 1;)
```

**Kali**

```
sudo snort -c local.rules -r ftp-png-gif.pcap -A full -l .
```

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

**Write a rule to detect failed FTP login attempts with "Administrator" username but a bad password or no password. What is the number of detected packets?**

**local.rules**

```
alert tcp any any <> any 21 (msg: "FTP Failed Login-Bad or No Password"; content:"331 Password"; sid: 100005; rev: 1;)
```

**Kali**

```
sudo snort -c local.rules -r ftp-png-gif.pcap -A full -l .
```

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

## Writing IDS Rules (PNG)

**Write a rule to detect the PNG file in the given pcap.**

**local.rules**

```
alert TCP any any <> any any (msg:"PNG File Dectected"; content:"|89 50 4E 47 0D 0A 1A 0A|"; sid:100002; rev:1;)
```

**Investigate the logs and identify the software name embedded in the packet.**

**Kali**

```
sudo snort -c local.rules -r ftp-png-gif.pcap -A full -l .
sudo snort -r snort.log* -X
```

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

**Write a rule to detect the GIF file in the given pcap.**

**local.rules**

```
alert TCP any any <> any any (msg:"GIF87a detected"; content:"|47 49 46 38 37 61|"; sid:10000003; rev:1;)
alert TCP any any <> any any (msg:"GIF89A detected"; content:"|47 49 46 38 39 61|"; sid:10000004; rev:1;)
```

**Investigate the logs and identify the software name embedded in the packet.**

**Kali**

```
sudo snort -c local.rules -r ftp-png-gif.pcap -A full -l .
sudo snort -r snort.log* -X
```

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

## Writing IDS Rules (Torrent Metafile)

**Write a rule to detect the torrent metafile in the given pcap.**

**local.rules**

```
alert TCP any any <> any any (msg:"Torrent Detected"; content:".torrent"; sid:10000003; rev:1;)
```

**What is the number of detected packets?**

**Kali**

```
sudo snort -c local.rules -r torrent.pcap -A full -l .
sudo snort -r snort.log* -X
```

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

## Troubleshooting Rule Syntax Errors

**Fix the syntax error in local-1.rules file and make it work smoothly.**

**local-1.rules**

```
alert TCP any 3372 -> any any (msg:"Troubleshooting 1"; sid:1000001; rev:1;)
```

**What is the number of the detected packets?**

**Kali**

```
sudo snort -c local-1.rules -r mx-1.pcap -A full -l .
```

<figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

**Fix the syntax error in local-2.rules file and make it work smoothly.**

**local-2.rules**

```
alert icmp any any -> any any (msg:"Troubleshooting 2"; sid:1000001; rev:1;)
```

**What is the number of the detected packets?**

**Kali**

```
sudo snort -c local-2.rules -r mx-1.pcap -A full -l .
```

<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

**Fix the syntax error in local-3.rules file and make it work smoothly.**

**local-3.rules**

```
alert icmp any any -> any any (msg:"ICMP Packet Found"; sid:1000001; rev:1;)
alert tcp any any -> any 80,443 (msg:"HTTPX Packet Found"; sid:1000002; rev:1;)
```

**What is the number of the detected packets?**

**Kali**

```
sudo snort -c local-3.rules -r mx-1.pcap -A full -l .
```

<figure><img src="../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>



**Fix the syntax error in local-4.rules file and make it work smoothly.**

**local-4.rules**

```
alert icmp any any -> any any (msg:"ICMP Packet Found"; sid:1000001; rev:1;)
alert tcp any any -> any 80,443 (msg:"HTTPX Packet Found"; sid:1000002; rev:1;)
```

**What is the number of the detected packets?**

**Kali**

```
sudo snort -c local-4.rules -r mx-1.pcap -A full -l .
```

<figure><img src="../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

**Fix the syntax error in local-5.rules file and make it work smoothly.**

**local-5.rules**

```
alert icmp any any <> any any (msg: "ICMP Packet Found"; sid:1000001; rev:1;)
alert icmp any any <> any any (msg: "Inbound ICMP Packet Found"; sid:1000002; rev:1;)
alert tcp any any -> any 80,443 (msg: "HTTPX Packet Found"; sid:1000003; rev:1;)
```

**What is the number of the detected packets?**

**Kali**

```
sudo snort -c local-5.rules -r mx-1.pcap -A full -l .
```

<figure><img src="../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

**Fix the syntax error in local-6.rules file and make it work smoothly.**

**local-6.rules**

```
alert tcp any any <> any 80  (msg: "GET Request Found"; content:"|47 45 5sudo snort -c local-6.rules -r mx-1.pcap -A full -l .4|"; sid:100001; rev:1;)
```

**What is the number of the detected packets?**

**Kali**

```
sudo snort -c local-6.rules -r mx-1.pcap -A full -l .
```

<figure><img src="../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

**Fix the syntax error in local-7.rules file and make it work smoothly.**

**local-7.rules**

```
alert tcp any any <> any 80  (msg:"No Message"; content:"|2E 68 74 6D 6C|"; sid: 100001; rev:1;)
```

**Kali**

```
sudo snort -c local-7.rules -r mx-1.pcap -A full -l .
```



## Using External Rules (MS17-010)

**Use the given rule file (local.rules) to investigate the ms1710 exploitation. What is the number of detected packets?**

**Kali**

```
sudo snort -c local.rules  -A full -l . -r ms-17-010.pcap
```

<figure><img src="../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

**Clear the previous log and alarm files. Use local-1.rules empty file to write a new rule to detect payloads containing the "\IPC$" keyword. What is the number of detected packets?**

**local-1.rules**

```
alert tcp any any -> any 445 (msg: "Exploit Detected!"; flow: to_server, established; content: "IPC$"; sid:2094285; rev: 3;)
```

**Kali**

```
sudo snort -c local-1.rules  -A full -l . -r ms-17-010.pcap
sudo snort -r snort.log* -X
```

<figure><img src="../../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

## Using External Rules (Log4j)

**Use the given rule file (local.rules) to investigate the log4j exploitation.**

**What is the number of detected packets?**

**Kali**

```
sudo snort -c local.rules  -A full -l . -r log4j.pcap
```

<figure><img src="../../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

\
**Investigate the log/alarm files. How many rules were triggered?**

<figure><img src="../../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

\
**Investigate the log/alarm files. What are the first six digits of the triggered rule sids?**

**Kali**

```
sudo snort -c local.rules  -A Full -l .  -r log4j.pcap
```

<figure><img src="../../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

**local-1.rules**

```
alert tcp any any -> any any (msg:"Payload 770-855 bytes"; dsize:770<>855; sid:100001; rev:1;)
```

**What is the number of detected packets?**

**Kali**

```
sudo snort -c local-1.rules  -A full -l . -r log4j.pcap
sudo snort -eX -r snort.log* | vi -
```

<figure><img src="../../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

**Output**

```
KGN1cmwgLXMgNDUuMTU1LjIwNS4yMzM6NTg3NC8xNjIuMC4yMjguMjUzOjgwfHx3Z2V0IC1xIC1PLSA0NS4xNTUuMjA1LjIzMzo1ODc0LzE2Mi4wLjIyOC4yNTM6ODApfGJhc2g=
```



**CyberChef:** [https://gchq.github.io/CyberChef/](https://gchq.github.io/CyberChef/)

<figure><img src="../../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>











