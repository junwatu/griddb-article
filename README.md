# GridDB 

## Installation

Ubuntu 18.04 WSL 2 on Windows 11

[https://docs.griddb.net/latest/gettingstarted/using-apt/#install-with-apt-get](https://docs.griddb.net/latest/gettingstarted/using-apt/#install-with-apt-get)

⚠️ GridDB `deb` package uses `systemd` but Ubuntu 18.04 on WSL 2 Windows 11 uses SysVinit so you need to enable `systemd` on Ubuntu WSL by editing file `/etc/wsl.conf` or create it if it doesn't exist.

```
[boot]
systemd=true
```

