# Ports



## **UDP/123  - NTP**

* NTP (Network Time Protocol) is used to set clocks on network computers.NTP is sent over UDP, which may be spoofed
* It can also be vulnerable to man-in-the-middle attacks
* NTP supports authentication
  * The public pool.ntp.org web servers do not use authentication

<figure><img src="../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

## **UDP/123  - SNTP**

* SNTP(Simple Network Time Protocol) is sometimes used rather than NTP&#x20;
  * The same basic protocol as NTP, but with much of the complexity removed&#x20;
  * SNTP is also less accurate than NTP&#x20;
  * Windows 2000 and XP's Windows Time service(W32Time) used SNTP&#x20;
  * Newer versions of Windows use NTP

## **UDP/161 & 162  - SNMP & SNMP Traps**

### **Difference between SNMP monitors and Traps**

| SNMP Monitors                                                                                                                                     | SNMP Traps                                                                                                                                                                                                                              |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Pull Model: OpManager sends SNMP request to the SNMP agent running on the monitored device and receives the response.                             | Push Model: Monitored device(SNMP agent) sends messages in the form of traps to the trap destination(OpManager)                                                                                                                         |
| Communication: both ways(UDP 161)                                                                                                                 | One way. Only from device to trap destination (UDP 162)                                                                                                                                                                                 |
| SNMP requests can be scheduled using monitoring intervals.                                                                                        | Traps are spontaneous. They will reach the destination as soon as they are generated.                                                                                                                                                   |
| Custom SNMP monitors can be created for the non default metrics. These monitors convert the raw SNMP response into a meaningful metric with unit. | Custom SNMP Trap processors are can be created for the new trap messages. They process the trap messages and convert them into meaningful alarms. If there is no trap processor, traps will be dumped under Alarms-->Unsolicited traps. |
| SNMP community string is mandatory to get a SNMP response                                                                                         | Community string is not mandatory to receive the trap message.                                                                                                                                                                          |

### Setup SNMPv3

&#x20;Create a SNMPv3 user in net-snmp configuration file

**OS**

```
service snmpd stop 
net-snmp-create-v3-user -ro -A '$PASSWORD1' -a SHA1 -X '$PASSWORD2' -x AES128 $USERNAME
service snmpd start
```

Test Locally

**OS**

```
snmpwalk -u $USERNAME -A '$PASSWORD1' -a SHA -X '$PASSWORD2' -x AES -l authPriv 127.0.0.1 -v3
```

\


## **TCP/1701 - L2TP**

* Layer Two Tunneling Protocol (L2TP) uses TCP port 1701 and is an extension of the Point-to-Point Tunneling Protocol. L2TP is often used with IPSec to establish a Virtual Private Network (VPN).
* Layer Two Tunneling Protocol (L2TP) is an extension of the Point-to-Point Tunneling Protocol (PPTP) used by an Internet service provider (ISP) to enable the operation of a virtual private network (VPN) over the Internet. L2TP merges the best features of two other tunneling protocols: PPTP from Microsoft and L2F from Cisco Systems. The two main components that make up L2TP are the L2TP Access Concentrator (LAC), which is the device that physically terminates a call and the L2TP Network Server (LNS), which is the device that terminates and possibly authenticates the PPP stream.

## **TCP/1723 - PPTP**

**Overview**\
• To allow PPTP tunnel maintenance traffic, open TCP 1723.\
• To allow PPTP tunneled data to pass through router, open Protocol ID 47.\
\
**How PPTP Works**\
PPTP is an outgrowth of PPP, and as such, is based on its authentication and encryption framework. Like all tunneling technologies, PPTP is used to encapsulate data packets, creating a tunnel for data to flow across an IP network.\
\
PPTP uses a client-server design (the technical specification is contained in Internet RFC 2637) that operates at Layer 2 of the OSI model. Once the VPN tunnel is established, PPTP supports two types of information flow:\
\
Control messages for managing and eventually tearing down the VPN connection. Control messages pass directly between VPN client and server.\
Data packets that pass through the tunnel, i.e. to or from the VPN client.\
People usually obtain the PPTP VPN server address information from their server administrator. Connection strings can either be a server name or an IP address.\
\
**PPTP Protocols**\
PPTP uses General Routing Encapsulation tunneling to encapsulate data packets. It uses TCP port 1723 and IP port 47 through the Transport Control Protocol. PPTP supports up to 128-bit encryption keys and Microsoft Point-to-Point Encryption standards.\
\
Tunneling Modes: Voluntary and Compulsory\
\
**The protocol supports two types of tunneling**\
Voluntary Tunneling: A type of tunneling that is initiated by the client (i.e Microsoft Windows) on an existing connection with a server.\
Compulsory Tunneling: A type of tunneling initiated by the PPTP server at the ISP, which requires the remote access server to create the tunnel.

