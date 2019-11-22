# Web-Project

## Prerequisites

- Ubuntu;
- Node.js;
- NPM modules:
  - mongodb;
  - socket.io;
  - request-json;
  - assert(build-in);
  - node-schedule;
  - emailjs(optional).
- PM2;
- MongoDB.

## How to deploy

1. Install Node.js:

   ```bash
   sudo apt-get update
   sudo apt-get install nodejs -y
   ```

2. Install `npm`:

   ```bash
   sudo apt-get install npm -y
   ```

3. Install `pm2` to manage processes:

   ```bash
   npm install pm2 --global
   ```

4. Install `mongodb` based on https://docs.mongodb.com/ ;

5. Create working directory:

   ```bash
   mkdir -p /data/release/web
   cd /data/release/web
   ```

6. Create `package.json` and `app.js`:

   ```json
   // package.json
   {
       "name": "weapp",
       "version": "1.0.0"
   }
   ```

7. Create `mongodb` directory to store data and logs:

```bash
mkdir -p /data/mongodb
mkdir -p /data/logs/mongodb
```

7. Start`mongodb`:

```bash
mongod --fork --dbpath /data/mongodb --logpath /data/logs/mongodb/app.log
```

8. Check if start successfully:

```bash
netstat -ltp | grep 27017
```

9. Add MongoDB user:

```bash
mongo
use web; # create dababase
db.createUser({ user: 'web', pwd: 'web', roles: ['dbAdmin', 'readWrite']}); # create user
```

10. Install mongo module:

```bash
cd /data/release/weapp
npm install connect-mongo wafer-node-session --save
```

## Some tips

- If you cannot connect the socket, update your firewall rule;