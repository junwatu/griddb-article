# GridDB 

## Installation

OS Ubuntu 20.04 WSL 2 on Windows 11

⚠️ GridDB deb package uses `systemd` but Ubuntu 20.04 on WSL 2 Windows 11 uses `SysVinit` so you need to enable `systemd` on Ubuntu WSL by editing file `/etc/wsl.conf` (create it if this file doesn't exist)

Inside your Ubuntu instance, add the following modification to `/etc/wsl.conf`[^1]

```
[boot]
systemd=true
```

Open Windows terminal to restart wsl with the following command

```
wsl --shutdown
```

then start wsl again with the command

```
wsl
```

then to install GridDB follow the installation instruction on [https://docs.griddb.net/latest/gettingstarted/using-apt/#install-with-apt-get](https://docs.griddb.net/latest/gettingstarted/using-apt/#install-with-apt-get).






[^1]: https://ubuntu.com/blog/ubuntu-wsl-enable-systemd
