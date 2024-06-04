# Writeup

This writeup was rushed to have it completed prior to RVAsec I will clean it up later this week.




Add the host to /etc/hosts for convenience
```
10.10.11.243    broker broker.htb
```

# Initial Enum

```
┌──(kali㉿kali)-[~]
└─$ nmap -sC -sV broker 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-06-02 00:09 EDT
Nmap scan report for broker (10.10.11.243)
Host is up (0.017s latency).
Not shown: 998 closed tcp ports (conn-refused)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 3e:ea:45:4b:c5:d1:6d:6f:e2:d4:d1:3b:0a:3d:a9:4f (ECDSA)
|_  256 64:cc:75:de:4a:e6:a5:b4:73:eb:3f:1b:cf:b4:e3:94 (ED25519)
80/tcp open  http    nginx 1.18.0 (Ubuntu)
|_http-server-header: nginx/1.18.0 (Ubuntu)
| http-auth: 
| HTTP/1.1 401 Unauthorized\x0D
|_  basic realm=ActiveMQRealm
|_http-title: Error 401 Unauthorized
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 7.49 seconds
```

First let's investigate the http site

![](https://gyrsec.github.io/zATTACHMENTS/Pasted%20image%2020240602002131.png)

we are presented with a login screen, trying admin:admin gets us through to ActiveMQ

![](https://gyrsec.github.io/zATTACHMENTS/Pasted%20image%2020240602002243.png)
Clicking on Manage ActiveMQ broker validates that we have admin privileges and shows that we are running version 5.15.15 with a copyright up to 2020, which feels a little old. Let's see if there are any useful exploits with searchsploit and google.
![](https://gyrsec.github.io/zATTACHMENTS/Pasted%20image%2020240602002852.png)
Searchsploit did not reveal anything too interesting but googling "activemq 5.15.15 cve" provides us with this github page https://github.com/SaumyajeetDas/CVE-2023-46604-RCE-Reverse-Shell-Apache-ActiveMQ

quickly running through the source code nothing looks suspicious, following along with the instructions we create our payload with msfvenom, modify the xml file to reflect our ip address, and catch the reverse shell with netcat
![](https://gyrsec.github.io/zATTACHMENTS/Pasted%20image%2020240602234613.png)
This is a limited shell so we first upgrade the shell: [[PRIVILEGE ESCALATION/OS/LINUX/UPGRADE SHELL|UPGRADE SHELL]]

![](https://gyrsec.github.io/zATTACHMENTS/Pasted%20image%2020240602235003.png)
in the user directory we find user.txt!
![](https://gyrsec.github.io/zATTACHMENTS/Pasted%20image%2020240602235447.png)
Initial enumeration
![](https://gyrsec.github.io/zATTACHMENTS/Pasted%20image%2020240603002319.png)
While doing some initial enumeration I noticed we can run nginx with sudo, double checking https://gtfobins.github.io/ does not immediately look exploitable but to see the help page I added the -h flag
![](https://gyrsec.github.io/zATTACHMENTS/Pasted%20image%2020240602235612.png)
![](https://gyrsec.github.io/zATTACHMENTS/Pasted%20image%2020240603224120.png)
interestingly -c appears to let us use our own config file, I copied /etc/nginx/nginx.conf and /etc/nginx/sites-enabled/default to the activemq user directory and we can run it but the config file gets deleted every few minutes. I created ~/nginx.conf.bak and ~/sites-enabled-bak/ so I can quickly restore the deleted files but those also got deleted. checking for cronjobs reveals that a script called "cleanup.sh" is running every 20 minutes, it is possible this is the culprit. Unfortunately I cannot read the bash script to be sure, for now we try bakconf and bakdefault in ~/nginx
![](https://gyrsec.github.io/zATTACHMENTS/Pasted%20image%2020240603224921.png)
I modify user to root, comment out `"include /etc/nginx/conf.d/*.conf;"` and change `include /etc/nginx/sites-enabled/*;` to `include /home/activemq/nginx/site;` I tried to modify /etc/nginx/sites-enabled/default first but it threw an error so I built /home/activemq/nginx/site off https://gist.githubusercontent.com/xameeramir/a5cb675fb6a6a64098365e89a239541d/raw/20a42070958edf3a4a54b31ac231ab64c01a4bda/default%2520nginx%2520configuration%2520filemodifying port and root location. While modifying I noticed that admin.broker.htb was listed and took note of it. After modifying the files and adding a test file I confirmed the site is working but the cleanup script removed the nginx folder, and backup folder I created. Screenshot is over port 82 as ports 80 and 81 were taken up at this point
![](https://gyrsec.github.io/zATTACHMENTS/Pasted%20image%2020240603230217.png)
So I once again copy the contents of the nginx config files, this time to my kali vm to modify there. Downloading the files to /tmp/test and running, the files are again removed. But redownloading and adding a test file gets us back to where we were.

If I have nginx running as the root user I am thinking either a reverse shell or reading /etc/shadow to crack the password. /etc/ssh/sshd_config has `PermitRootLogin yes` so I will try grabbing /etc/shadow first. I modify root to point to /etc/ in default `root /etc/;` redownload the files into /tmp with an updated port and succesfully download /etc/shadow
![](https://gyrsec.github.io/zATTACHMENTS/Pasted%20image%2020240603233756.png)

the root hash is encrpyted with yescrypt and john does not crack after a couple of minutes. I wonder what is in that script from earlier?
![](https://gyrsec.github.io/zATTACHMENTS/Pasted%20image%2020240604002518.png)
Nothing that helps but it confirms my suspicion that it is removing files every 20 minutes. Checking the .ssh folder and I do not find any ssh keys, but we can create our own with `ssh-keygen -f broker`. By modifying default I can enable the put method and add my own ssh key file using https://nginx.org/en/docs/http/ngx_http_dav_module.html and https://stackoverflow.com/questions/55787223/upload-file-to-nginx-with-curl as references. After some trial and error I end up with
![](https://gyrsec.github.io/zATTACHMENTS/Pasted%20image%2020240604011757.png)
upload, start nginx as root, upload the ssh public key with `curl -T broker.pub http://broker.htb:8096/upload/broker.pub`
ssh with `ssh -i ./broker root@broker.htb` and get root!
While I could have grabbed the root.txt file earlier now that I have a root shell I just cat it.
![](https://gyrsec.github.io/zATTACHMENTS/Pasted%20image%2020240604012250.png)