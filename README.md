# config
Configuration for unlimited history, completion, SSH client/server keep alive, uploading ssh certs etc.

# SSH server side "keep alive"
- `vim /etc/ssh/sshd_config`, add:
```
TCPKeepAlive yes
ClientAliveInterval 299
ClientAliveCountMax 299
```
- `service sshd restart`.


# SSH client side "keep alive"
- `vim /etc/ssh/ssh_config`, ensure:
```
Host *
    ServerAliveInterval 299
    ServerAliveCountMax 299
```


# Bash history & completion tricks
- `cp ~/.bash_history ~/.history`
- `vim ~/.bashrc`, add:
```
# History stuff
export HISTFILESIZE=
export HISTSIZE=
export HISTFILE=~/.history
export HISTTIMEFORMAT="[%F %T] "
export PROMPT_COMMAND="history -a; history -c; history -r"
export HISTCONTROL=ignoredups:ignorespace:erasedups
```
