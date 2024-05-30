# KEEPASS DATABASE
#extract_hash
`keepass2john ./Database.kdbx > Keepasshash.txt`

#john
`john --wordlist=/usr/share/wordlists/rockyou.txt Keepasshash.txt`

#hashcat
```sh
remove db name from Keepasshash.txt
hashcat -m 13400 -a 0 ./Keepasshash.txt ~/wordlists/rockyou.txt
```