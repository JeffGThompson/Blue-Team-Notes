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

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

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
```

```
sudo snort -r snort.log* -X
```

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

















