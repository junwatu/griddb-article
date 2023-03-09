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

GridDB node-api is built using node-addon-api so to using it you need to install it from npm or clone the GridDB node-api repository

```
git clone git@github.com:griddb/node-api.git
cd node-api
npm install
```

if there is an error message `gyp ERR! stack Error: not found: make` then you should install the `build-essentials` package in Ubuntu and if everything success you will get a `griddb.node`

```zsh
equan@GenAI:~/node-api$ ls -l
total 1200
-rw-r--r-- 1 equan equan 181395 Mar  9 05:09 CLA_rev1.1.pdf
-rw-r--r-- 1 equan equan  11358 Mar  9 05:09 LICENSE
-rw-r--r-- 1 equan equan   1936 Mar  9 05:09 README-NPM.md
-rw-r--r-- 1 equan equan   2857 Mar  9 05:09 README.md
-rw-r--r-- 1 equan equan   2178 Mar  9 05:09 binding.gyp
drwxr-xr-x 5 equan equan   4096 Mar  9 05:23 build
drwxr-xr-x 3 equan equan   4096 Mar  9 05:09 docs
-rw-r--r-- 1 equan equan   1846 Mar  9 05:09 griddb-node-api.js
-rwxr-xr-x 3 equan equan 982040 Mar  9 05:24 griddb.node
drwxr-xr-x 2 equan equan   4096 Mar  9 05:09 include
drwxr-xr-x 3 equan equan   4096 Mar  9 05:10 node_modules
-rw-r--r-- 1 equan equan    852 Mar  9 05:23 package-lock.json
-rw-r--r-- 1 equan equan    826 Mar  9 05:09 package.json
drwxr-xr-x 2 equan equan   4096 Mar  9 05:09 sample
drwxr-xr-x 2 equan equan   4096 Mar  9 05:09 src
```

Before code the Node.js application you need to include the `gridbd.node` in `NODE_PATH` with this command

```
$ export NODE_PATH=$(pwd)
```


[^1]: https://ubuntu.com/blog/ubuntu-wsl-enable-systemd
[^2]: https://github.com/nodesource/distribution

