---
layout: single
title: Installation
permalink: /installation/

toc: true
toc_sticky: true
sidebar:
  nav: "docs"
---

## Downloading

Download the entire project folder from the GitHub repository and open it in your code editor if you want to use it as-is. If you’d like to customize the software to suit your needs, feel free to fork the repository. For general improvements, you can clone the repo and submit a pull request.

**Github**
[SentinelIS Information Security Management System](https://github.com/SentinelIS/SentinelIS-Core)

**Clone** 
``` bash
git clone https://github.com/SentinelIS/SentinelIS-Core.git
```

## Setup Guide

### Step 1: Ports

Before starting the setup, please make sure that all required ports are free and not being used by any other software. You can change the ports for your local installation if needed. However, if you plan to contribute to this project, changing the ports is not allowed.

**Show All Used Ports**
```powershell
netstat -aon | Sort-Object
```

By default, the entire project runs on `localhost`. You can change this if needed. The default ports are:

- `3000`: Express server for login and setup
- `4000`: Apollo server for GraphQL
- `5137`: .NET Server for Chatsystem
- `3307:3306`: MySQL database
- `27018:27017`: MongoDB database
- `8081:8080`: SQLite database

For further Information about the databases see: Database Design

### Step 2: Create .env files

For all the different databases and services, you will need to set up a `.env` file containing all your keys and credentials. Please make sure to follow **exactly** this format:

```yaml
MYSQL_HOST=localhost
MYSQL_PORT=3307
MYSQL_ROOT_PASSWORD= ..
MYSQL_DATABASE= ..
MYSQL_USER= ..
MYSQL_PASSWORD= ..

MONGO_INITDB_ROOT_USERNAME= ..
MONGO_INITDB_ROOT_PASSWORD= ..
MONGO_INITDB_DATABASE= ..
MONGO_CONNECTION_STRING= ..

SQLITE_DB_PATH=/sqlite/data/mydb.sqlite
SQLITE_GUI_PORT=8081

JWT_SECRET= ..
```

**Important:** Make sure that the JWT Secret is at least 16 characters long, better 32!

Please make sure that the following directories contain a `.env` file:

- `SentinelIS-Core/docker`: This directory must contain the main `.env` file. If it is missing, the entire application will not work.
- `SentinelIS-Core/backend/main/node`: The server files require a `.env` file unless you plan to use fallback defaults or hardcode the values. Both of which are not recommended.
- `SentinelIS-Core/backend/LiveChatApp`: The server expects a `.env` file for the JWT Token and for the database connections.
- `SentienlIS-Core/backend/main/testing`: The Python test scripts also expect a `.env` file to be present.

You can use system-wide environment variables instead of separate `.env` files, but this would require modifying all connection configurations accordingly.

For all database connections, Python test scripts are available. You can use these scripts to avoid testing the connections manually. If you choose not to use the Python scripts, you can safely delete the `testing/` directory in the `backend` folder.