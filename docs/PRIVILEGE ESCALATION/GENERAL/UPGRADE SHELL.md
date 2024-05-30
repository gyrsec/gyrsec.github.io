# UPGRADE SHELL
#python

- Spawning **bash** with **python**:

```ruby
python -c 'import pty; pty.spawn("/bin/bash")'
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

- Backgrounding the _remote_ shell with **CTRL-Z**:

```ruby
user@remote:~$ ^Z
```

- Getting ROWS and COLS within current terminal window:

```bash
user@local:~$ stty -a | head -n1 | cut -d ';' -f 2-3 | cut -b2- | sed 's/; /\n/'
```

- Ignoring hotkeys in the _local_ shell and getting back to the _remote_:

```bash
user@local:~$ stty raw -echo; fg
```

- Setting correct size for the _remote_ shell (where `ROWS` and `COLS` are the values from the 3rd bullet):

```sql
user@remote:~$ stty rows ROWS cols COLS
```

- Adding some colors:

```ruby
user@remote:~$ export TERM=xterm-256color
```

- Reloading bash to apply the TERM variable:

```ruby
user@remote:~$ exec /bin/bash
```

src: slightly modified from [snovvcrash](https://forum.hackthebox.com/t/obtaining-a-fully-interactive-shell/128/22?u=gyrsec)