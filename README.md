# Web-Project

A book management web project demo named `Bibliosoft` using `Node.js`.

# Screen shots

|  ![](doc/reader_index.png)   | ![](doc/reader_login.png) |
| :--------------------------: | :-----------------------: |
| ![](doc/librarian_index.png) | ![](doc/admin_index.png)  |

# Backlog

## Product Backlog

### Admin

- 登入&登出
- 修改密码
- 添加librarian，密码默认为00010001
- 管理（编辑/删除）librarian
- 修改书籍逾期罚金（默认为1元/天）
- 修改书籍归还期限（默认为30天）
- 修改读者注册时缴纳的保证金（默认为300元）
- 搜索librarian，查看librarian列表
- 帮助librarian找回密码

### Librarian

- 登入&登出
- 修改密码
- 注册reader，手机号为用户名，密码默认为12345678
- 管理（编辑/删除）reader，删除时须确保罚金已还清&书已归还（删除条件未调整）
- 加书（位置和价格必需），生成条形码（位置未从后端读入）
- 编辑书籍信息
- 删除书籍，精确到书籍&副本，保存和浏览删除书籍的操作记录（包含操作人）
- 搜书
- 借书（一个账号最多同时借阅3本书）
- 还书
- 浏览reader的借书、还书、罚金记录（未显示当前待支付金额）
- 浏览图书馆收入记录（按天/月/年），收入包含保证金和罚金
- 添加/编辑/删除主页的公告
- 添加/编辑书籍类别
- 添加/编辑/删除位置
- 在admin的帮助下找回密码

### Reader

- 登入/登出
- 修改个人信息和密码
- 查书
- 预约2小时
- 浏览借书、还书、缴纳罚金记录和当前待支付罚金
- 书籍到期前收到邮件提醒
- 通过邮件找回密码

## 其他

* 须包含英文界面
* 使用产品LOGO
* 须有页眉页脚
* 主页须有：搜索、登录、公告
* 须测试所有输入的空值和错误值
* 隐藏Admin登录界面

# Prerequisites

- Windows;
- Nginx;
- MongoDB;
- Node.js;
- NPM modules:
  - PM2
  - mongodb;
  - socket.io;
  - request-json;
  - node-schedule;
  - emailjs.

# How to deploy

## Install dependencies

- Visit www.mongodb.com and download and install `mongoDB server`;

- Visit  http://nginx.org/en/download.html and download and install `Nginx`;

- Visit  https://nodejs.org/en/  and download and install `Node.js` (`NPM` will also install automatically);

- Create back-end directory and enter it:

  ```bash
  mkdir bibliosoft
  cd bibliosoft
  ```

  then **copy there all the stuffs in`back_end` directory**.

- Install `PM2` globally:

  ```bash
  npm install pm2 -g
  ```

- Install `mongodb`, `socket.io`, `request-json`, `node-schedule`, `emailjs` locally (**not recommended**):

  ```bash
  npm install --save mongodb socket.io request-json node-schedule emailjs
  ```

  or just install by `package.json` (**recommended**):

  ```bash
  npm install
  ```

## Initialization

- Start `mongoDB` server:

  ```bash
  mongod  --dbpath <your path such as C:\Programs\MongoData> --logpath <your log path such as C:\Programs\MongoData\app.log>
  ```

- Start `mongoDB` client:

  ```bash
  mongo
  ```

  enter the interaction mode and execute following code to create database `Bibliosoft`:

  ```
  use Bibliosoft
  ```

  initialize:

  ```bash
  db.getCollection("accounts").drop()
  db.getCollection("admin").drop()
  db.getCollection("librarian").drop()
  db.getCollection("reader").drop()
  db.getCollection("books").drop()
  db.getCollection("copies").drop()
  db.getCollection("borrows").drop()
  db.getCollection("reserve").drop()
  db.getCollection("session").drop()
  db.getCollection("librarianOperation").drop()
  db.getCollection("income").drop()
  db.getCollection("news").drop()
  db.getCollection("restorePassword").drop()
  db.getCollection("config").drop()
  
  db.createCollection("accounts")
  db.createCollection("admin")
  db.createCollection("librarian")
  db.createCollection("reader")
  db.createCollection("books")
  db.createCollection("copies")
  db.createCollection("borrows")
  db.createCollection("reserve")
  db.createCollection("session")
  db.createCollection("librarianOperation")
  db.createCollection("income")
  db.createCollection("news")
  db.createCollection("restorePassword")
  db.createCollection("config")
  
  db.getCollection("accounts").insert({"username":"admin", "password": "admin", "type": "admin"})
  
  db.getCollection("location").insert({location: "1-01-01"})
  db.getCollection("location").insert({location: "1-01-02"})
  
  db.getCollection("type").insert({type: "Music"});
  db.getCollection("type").insert({type: "Art"});
  db.getCollection("type").insert({type: "Science"});
  
  db.getCollection("globalVar").insert({var_name:"bar_code", "bar_code": 7563287654293});
  db.getCollection("globalVar").insert({var_name:"librarian", "librarian":  1000020});
  
  db.getCollection("config").insert({varname:"config", "security":300, "limit": 30, "exceed": 1, "maxnum": 3, "reserve": 2});
  ```

  then you get a administration user `admin` and password is `admin`!

- Start front-end:

  - Copying all the stuffs from `front-end` to the `html` directory of  `Nginx`;
  - Start `Nginx`.

- Start back-end by entering `bibliosoft` directory and executing following:

  ```bash
  pm2 start app.js
  ```

  or restart:

  ```bash
  pm2 restart app
  ```

  You also can monitor the logs by:

  ```bash
  pm2 logs
  ```

  and flush them by:

  ```bash
  pm2 flush
  ```

# Test

Open your browser and enter 

http://localhost/admin_login/admin_login.html 

to test `admin` login and enter

 http://localhost/reader_login/login.html 

to test `librarian` login and enter

 http://localhost/reader/login.html 

to test `reader` login.

# Some tips

- If you cannot connect the socket, update your server's firewall rule;