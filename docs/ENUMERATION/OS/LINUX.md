# LINUX
#local_enum

#whoami
``` bash
id
```

#distribution
``` bash
cat /etc/issue
cat /etc/*release
```

#kernel
``` bash
uname -a
cat /proc/version
```

#environment_variables 
``` bash
env
set
cat /etc/profile
cat /etc/bashrc
cat ~/.bash_profile
cat ~/.bashrc
cat ~/.bash_logout
cat ~/.zshrc
```

#ssh
``` bash
DSA
	
~/.ssh/id_dsa.pub
~/.ssh/id_dsa

RSA

~/.ssh/id_rsa.pub
~/.ssh/id_rsa

ECDSA

~/.ssh/id_ecdsa.pub
~/.ssh/id_ecdsa

Ed25519 (Edwards-curve DSA)

~/.ssh/id_ed25519.pub
~/.ssh/id_ed25519
```

#crack
``` bash
ssh2john.py id_rsa > id_rsa.hash
john id_rsa.hash
```