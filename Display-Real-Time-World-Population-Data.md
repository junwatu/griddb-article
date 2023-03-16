# Display World Population Data With Mapbox, Node.js and GridDB

In this blog, we will show you how to display world population data from [worldometers](https://www.worldometers.info/) using React, Mapbox GL JS, Node.js, and GridDB with a TimeSeries container.

The flow for this project can be breakdown into a few steps:

## Data Acquisition

First, we need to get real-time data from [worldometers](https://www.worldometers.info/). This can be done by scrapping the website and getting the data that we need. The data will be extracted at regular intervals to keep it up-to-date.

## Back-end Development

We will use Node.js to code the server-side application server.

> Why Node.js? JavaScript is the lingua franca for full-stack application development, so it's the obvious choice.

The application server we make is API-based, and Node.js will interact with GridDB for data storage, handle retrieval data from worldometer, and handle requests and responses from the client UI.

## Front end Development

We use React.js to create the user interface. To display the world population data visually, we'll use Mapbox GL JS, a powerful mapping library. This library enables the creation of interactive, customizable maps. We'll integrate Mapbox GL JS with our React application to render a world map with markers or overlays representing the population data.

## Setup

Before we code the application, we need to set up the software and tools for development. We use Ubuntu 20.04 on WSL 2 on Windows 11 OS.

## GridDB

[GridDB](https://griddb.net/en/)™ is a highly scalable, in-memory NoSQL time-series database optimized for IoT and Big Data. What's important to note is it has two types of container categories:

### Collection Containers

This type of container is similar to a traditional relational database. The data is stored as key values, and the collection container support basic CRUD (Create, Read, Update, and Delete) operation.

### TimeSeries Containers

This container is designed explicitly for managing time-series data, a sequence of data points indexed by time. Each record in a TimeSeries container has a timestamp, which serves as its unique key, and the data in this container is "append only" except upon deletion if requested.

### Installation

⚠️ GridDB deb package uses `systemd` but Ubuntu 20.04 on WSL 2 Windows 11 uses `SysVinit` so you need to enable `systemd` on Ubuntu WSL by editing file `/etc/wsl.conf` (create it if this file doesn't exist)

Inside your Ubuntu instance, add the following modification to `/etc/wsl.conf`[^1]

```ini
[boot]
systemd=true
```

Open Windows terminal to restart wsl with the following command

```powershell
wsl --shutdown
```

then start wsl again with the command

```powershell
wsl
```

then to install GridDB follow the installation instruction on [https://docs.griddb.net/latest/gettingstarted/using-apt/#install-with-apt-get](https://docs.griddb.net/latest/gettingstarted/using-apt/#install-with-apt-get).

## Node.js

Installation[^2] Node.js 18 LTS

```zsh
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash - &&\
sudo apt-get install -y nodejs
```

We will be using [griddb node-api](https://github.com/griddb/node-api) to connect our application with GridDB but before that wes should install the [griddb c client](https://github.com/griddb/c_client).

The GridDB C Client provides a C interface for GridDB.

```zsh
wget https://github.com/griddb/c_client/releases/download/v5.0.0/griddb-c-client_5.0.0_amd64.deb
sudo dpkg -i griddb-c-client_5.0.0_amd64.deb
```

### GridDB node-api

GridDB node-api is built using node-addon-api so to using it you need to install it from npm or clone the GridDB node-api repository

```zsh
git clone git@github.com:griddb/node-api.git
cd node-api
npm install
```

if there is an error message like this

```zsh
gyp ERR! stack Error: not found: make
```

that's means you should install the `build-essentials` package in Ubuntu and if everything success you will get a `griddb.node`

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

```zsh
export NODE_PATH=$(pwd)
```

[^1]: https://ubuntu.com/blog/ubuntu-wsl-enable-systemd
[^2]: https://github.com/nodesource/distribution
