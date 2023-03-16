[GridDB](https://griddb.net/en/)™ is a highly scalable, in-memory NoSQL time-series database optimized for IoT and Big Data. What's important to note is it has two types of container categories:

### Collection Containers

This type of container is similar to a traditional relational database. The data is stored as key values, and the collection container support basic CRUD (Create, Read, Update, and Delete) operation.

### TimeSeries Containers

This container is designed explicitly for managing time-series data, a sequence of data points indexed by time. Each record in a TimeSeries container has a timestamp, which serves as its unique key, and the data in this container is "append only" except upon deletion if requested.

## The Project

In this blog, we will show you how to display world population data from [worldometers](https://www.worldometers.info/) in real time using React, Mapbox GL JS, Node.js, and GridDB with a TimeSeries container.

The flow for this project can be breakdown into a few steps:

### Data Acquisition

First, we need to get real-time data from [worldometers](https://www.worldometers.info/). This can be done by scrapping the website and getting the data that we need. The data will be extracted at regular intervals to keep it up-to-date.

### Back-end Development

We will use Node.js to code the server-side application server.

> Why Node.js? JavaScript is the lingua franca for full-stack application development, so it's the obvious choice.

The application server we make is API-based, and Node.js will interact with GridDB for data storage, handle retrieval data from worldometer, and handle requests and responses from the client UI.

### Front end Development

We use React.js to create the user interface. To display the world population data visually, we'll use Mapbox GL JS, a powerful mapping library. This library enables the creation of interactive, customizable maps. We'll integrate Mapbox GL JS with our React application to render a world map with markers or overlays representing the population data.

## Setup

Before we code the application, we need to set up the software and tools for development. For this project, we use Windows 11 22H2 for development.

### Node.js LTS

We can use a windows package manager like [winget](https://github.com/microsoft/winget-cli) or just install Node.js 18 LTS version with a windows installer from [nodejs.org](https://nodejs.org/dist/v18.15.0/node-v18.15.0-x64.msi)

### Docker Desktop

The reason why we need to install [Docker Desktop](https://www.docker.com/products/docker-desktop/) is that we need the GridDB Docker version for fast and easy installation. In the long term, it will be easier if we want to deploy the project on the cloud.

### GridDB

To install GridDB via docker, you can use this command on the windows terminal

```bash
docker pull griddbnet/griddb
```

```
docker run --hostname=localhost -d -t  griddbnet/griddb
```
