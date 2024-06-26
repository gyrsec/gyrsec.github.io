# Writeup

add to /etc/hosts
`10.10.10.100    active active.htb`

`nmap -sC -sV active`

```
Nmap scan report for active (10.10.10.100)
Host is up (0.021s latency).
Not shown: 983 closed tcp ports (conn-refused)
PORT      STATE SERVICE       VERSION
53/tcp    open  domain        Microsoft DNS 6.1.7601 (1DB15D39) (Windows Server 2008 R2 SP1)
| dns-nsid: 
|_  bind.version: Microsoft DNS 6.1.7601 (1DB15D39)
88/tcp    open  kerberos-sec  Microsoft Windows Kerberos (server time: 2024-06-25 04:08:55Z)
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
389/tcp   open  ldap          Microsoft Windows Active Directory LDAP (Domain: active.htb, Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds?
464/tcp   open  kpasswd5?
593/tcp   open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp   open  tcpwrapped
3268/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: active.htb, Site: Default-First-Site-Name)
3269/tcp  open  tcpwrapped
49152/tcp open  msrpc         Microsoft Windows RPC
49153/tcp open  msrpc         Microsoft Windows RPC
49154/tcp open  msrpc         Microsoft Windows RPC
49155/tcp open  msrpc         Microsoft Windows RPC
49157/tcp open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
49158/tcp open  msrpc         Microsoft Windows RPC
Service Info: Host: DC; OS: Windows; CPE: cpe:/o:microsoft:windows_server_2008:r2:sp1, cpe:/o:microsoft:windows

Host script results:
| smb2-time: 
|   date: 2024-06-25T04:09:51
|_  start_date: 2024-06-25T03:44:14
| smb2-security-mode: 
|   2:1:0: 
|_    Message signing enabled and required
```

2008 r2, I checked for Eternal Blue but it isn't quite that easy. 

after some basic enum against active directory I find the Replication share is accessible

![](https://gyrsec.github.io/zATTACHMENTS/Pasted%20image%2020240625234413.png)


exploring the fileshare I find a few files, but the relevant one is Groups.xml 
![](https://gyrsec.github.io/zATTACHMENTS/Pasted%20image%2020240625235352.png)


Hacktricks provides a good breakdown [here](https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#cached-gpp-pasword) but the short of it is that Windows used to allow for deploying local administrator accounts with Group Policy Preferences, using a known key top encrypt the passwords

![](https://gyrsec.github.io/zATTACHMENTS/Pasted%20image%2020240626001626.png)

I tried psexec with the compromised user but again it won't be that easy

![](https://gyrsec.github.io/zATTACHMENTS/Pasted%20image%2020240626001346.png)

The reason psexec is not working is that we do not have access to ADMIN$

![](https://gyrsec.github.io/zATTACHMENTS/Pasted%20image%2020240626002349.png)

we can get the user flag through the Users share but the account name SVC_TGS sounds like a hint for kerberoasting, and grabbing a flag without a shell is not as satisfying. I used impacket-GetUserSPNS for kerberoasting

![](https://gyrsec.github.io/zATTACHMENTS/Pasted%20image%2020240626005214.png)

and hashcat makes quick work of cracking
`hashcat -m 13100 --force -a 0 hashes.kerberoast /usr/share/seclists/Passwords/Leaked-Databases/rockyou.txt`

![](https://gyrsec.github.io/zATTACHMENTS/Pasted%20image%2020240626005347.png)

you can use `hashcat --show [hash file]` to vire previously cracked passwords, using the administrator password with psexec we get a remote shell as system!

![](https://gyrsec.github.io/zATTACHMENTS/Pasted%20image%2020240626005844.png)

All in all a very easy box but it is a nice break from all the hackthebox vms I have been going through lately which start with a web application