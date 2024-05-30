# SSH KEY FILES
```
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
```unknown
ssh2john.py id_rsa > id_rsa.hash
john id_rsa.hash
```