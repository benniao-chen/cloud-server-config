curl --silent --location https://rpm.nodesource.com/setup_8.x | sudo bash -
yum install nodejs -y
npm install pm2 --global
npm install express --save

pm2 start app.js
pm2 logs
pm2 restart app

yum install nginx -y

//设置反代理 /etc/nginx/conf.d
ssl.conf

//重启nginx服务
nginx -s reload

//安装mongodb
yum install mongodb-server mongodb -y

//操作mongodb
mkdir -p /data/mongodb
mkdir -p /data/logs/mongodb
mongod --fork --dbpath /data/mongodb --logpath /data/logs/mongodb/weapp.log

//检测是否启动
netstat -ltp | grep 27017

//进入mongo命令行
mongo

//创建用户
use weapp;
db.createUser({ user: 'weapp', pwd: 'weapp-dev', roles: ['dbAdmin', 'readWrite']});

//实现小程序的会话功能，我们需要安装 connect-mongo 和 wafer-node-session
npm install connect-mongo wafer-node-session --save

//实现socket功能
npm install ws --save

//使用 co 进行协程管理
npm install co --save

//修改完app.js，重启node服务
pm2 restart app

//修改完ssl.conf，重启nginx服务
nginx -s reload

