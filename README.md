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

## Node.js

Installation[^2] Node.js 18 LTS

```
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash - &&\
sudo apt-get install -y nodejs
```

We will be using [griddb node-api](https://github.com/griddb/node-api) to connect our application with GridDB but before that wes should install the [griddb c client](https://github.com/griddb/c_client).

The GridDB C Client provides a C interface for GridDB.

```
wget https://github.com/griddb/c_client/releases/download/v5.0.0/griddb-c-client_5.0.0_amd64.deb
sudo dpkg -i griddb-c-client_5.0.0_amd64.deb
```

### GridDB node-api



[^1]: https://ubuntu.com/blog/ubuntu-wsl-enable-systemd
[^2]: https://github.com/nodesource/distributions/blob/master/README.md
