# SMTP
https://book.hacktricks.xyz/network-services-pentesting/pentesting-smtp

#nmap

```sh
nmap -p25 --script smtp-commands [ip]
nmap -p25 --script smtp-open-relay [ip] -v
```

#NTLM_auth_information_disclosure

https://medium.com/swlh/internal-information-disclosure-using-hidden-ntlm-authentication-18de17675666`

```sh
telnet example.com 587
```

#connect

```sh
telnet [ip] 25
```

#commands

```sh
ehlo var - first command on connection, handshake + show extended information
helo var - same but less info
```

#verify_username_exists

```sh
MAIL FROM:test@test.org
RCPT TO:admin

VRFY admin
```

#autocomplete_for_server_domain

```sh
MAIL FROM: me
250 2.1.0 me@PRODSERV01.somedomain.com....Sender OK250 2.1.0 me@PRODSERV01.somedomain.com....Sender OK
```