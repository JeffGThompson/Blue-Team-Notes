# Snort Challenge - Live Attacks

**Room Link:** [https://tryhackme.com/room/snortchallenges2](https://tryhackme.com/room/snortchallenges2)

**Kali**

```
sudo gedit /etc/snort/rules/local.rules &
```

**local.rules**

```
drop tcp any any -> any any (sid: 1000001;)
```

**Stop the attack and get the flag (which will appear on your Desktop)**

**Kali**

```
sudo snort -c /etc/snort/snort.conf -q -Q --daq afpacket -i eth0:eth1 -A full
```



**What is the name of the service under attack?**

**Kali**

```
sudo snort -c /etc/snort/snort.conf -q -Q --daq afpacket -i eth0:eth1 -A console
```

<figure><img src="../../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

**What is the used protocol/port in the attack?**

**Kali**

```
sudo snort -c /etc/snort/snort.conf -q -Q --daq afpacket -i eth0:eth1 -A console
```

<figure><img src="../../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

**Stop the attack and get the flag (which will appear on your Desktop)**

**Kali**

```
sudo gedit /etc/snort/rules/local.rules &
```

**local.rules**

```
drop tcp any any -> any any (sid: 1000001;)
```

**Kali**

```
sudo snort -c /etc/snort/snort.conf -q -Q --daq afpacket -i eth0:eth1 -A full
```



**What is the name of the service**

**Kali**

```
sudo snort -c /etc/snort/snort.conf -q -Q --daq afpacket -i eth0:eth1 -A console
```

<figure><img src="../../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>







































