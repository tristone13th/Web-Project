# Web-Project

## Prerequisites

- Node.js;
- NPM;
- MongoDB.

## How to deploy

1. Install Node.js:

   ```bash
   sudo apt-get update
   sudo apt-get install nodejs -y
   ```

2. Install NPM:

   ```bash
   sudo apt-get install npm -y
   ```

3. Install `mongodb` based on https://docs.mongodb.com/ ;

4. Create `mongodb` directory to store data and logs:

   ```bash
   mkdir -p /data/mongodb
   mkdir -p /data/logs/mongodb
   ```

5. Start`mongodb`:

   ```bash
   mongod --fork --dbpath /data/mongodb --logpath /data/logs/mongodb/app.log
   ```

6. Check if start successfully:

   ```bash
   netstat -ltp | grep 27017
   ```

   