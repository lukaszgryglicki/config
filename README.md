# config
Configuration for unlimited history, completion, SSH client/server keep alive, uploading ssh certs etc.

# SSH server side "keep alive"
- `vim /etc/ssh/sshd_config`, add (this is how ofyten and how many times server will send IDLE packages to the clinet):
```
TCPKeepAlive yes
ClientAliveInterval 299
ClientAliveCountMax 299
```
- `service sshd restart` and/or `sudo systemctl restart ssh.service`.
- NOTE: that server sends broken pipe if no IDLE package is received from client after `ClientAliveInterval` - so this must be either skipped or set to a value higher than `ServerAliveInterval` in SSH client config.


# SSH client side "keep alive"
- `vim /etc/ssh/ssh_config`, ensure (this is how often and how many times client will send IDLE packages to the server):
```
Host *
    ServerAliveInterval 270
    ServerAliveCountMax 290
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


# GRUB
Add this to `` /etc/default/grub ``:
```
GRUB_CMDLINE_LINUX_DEFAULT="nomodeset"
GRUB_CMDLINE_LINUX=""
```
