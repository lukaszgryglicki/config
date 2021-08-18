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

# Auto completion of history commands on up/down keys
- `vim ~/.inputrc`, add:
```
"\e[A": history-search-backward
"\e[B": history-search-forward
```

# Upload SSH keys to the server
- One liner: `ssh-copy-id -i ~/.ssh/id_rsa.pub user@host`.
- Or
- Generate a public key (only if you don't have it yet): `ssh-keygen -o`
- Copy your public key: `~/.ssh/id_rsa.pub`.
- SSH to a remote server (using password): `ssh user@host`.
- Add a key: `vim ~user/.ssh/authorized_keys`
- Set correct perms: `chmod 700 ~user/.ssh && chmod 600 ~user/.ssh/authorized_keys`.
