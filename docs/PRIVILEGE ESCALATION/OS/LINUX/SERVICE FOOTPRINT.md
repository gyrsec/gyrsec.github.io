# SERVICE FOOTPRINT
#running_processes
```
# SERVICE FOOTPRINT
watch -n 1 "ps -aux | grep pass"
```

#tcpdump
```
# grep traffic through loopback for "pass"
sudo tcpdump -i lo -A | grep "pass"
```