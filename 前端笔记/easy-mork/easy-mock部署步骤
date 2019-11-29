### Centos7 64位 安装 Node.js v8.x( 注意:不支持 v10.x）
参考: https://github.com/easy-mock/easy-mock/blob/dev/README.zh-CN.md

1. 将node官网下载的 node-v8.11.1-linux-x64.tar.xz 上传至服务器 

2. 解压xz文件
```shell 
xz -d node-v8.11.1-linux-x64.tar.xz
```
3. 解压tar文件
```shell 
tar -xvf node-v8.11.1-linux-x64.tar
```
4. 目录重命名
```shell 
mv node-v8.11.1-linux-x64 node
```
5. 移动目录到/usr/local下
```shell 
mv node /usr/local/
```
6. 配置环境变量
```shell 
vi /etc/profile
```
6.1 填写以下内容
```shell 
export NODE_HOME=/usr/local/node 
export PATH=$NODE_HOME/bin:$PATH
```
6.2 执行命令让环境变量生效
```shell 
source /etc/profile
```
7. 查看node版本看是否安装成功
```shell 
node -v
```

### 安装 Mongodb
#### 创建并编辑文件：
```shell 
vi /etc/yum.repos.d/mongodb-org-3.2.repo
```
内容如下：
```properties
[mongodb-org-3.2]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.2/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.2.asc
```
#### 安装
```shell
yum install -y mongodb-org
```
#### 启动
```shell
systemctl start mongod
```
###  安装Redis
#### 下载fedora的epel仓库
```shell
yum install epel-release
```
#### 下载安装redis
```shell
yum install redis
```
#### 启动redis服务
```shell
systemctl start redis
```
###  本地部署easy-mock
1. 项目下载地址：https://github.com/easy-mock/easy-mock
2. 将 easy-mock-dev.zip上传至服务器

3. 安装 zip 和 unzip
```shell
yum install zip unzip
```
4. 解压
```shell
unzip easy-mock-dev.zip
```
5. 进入其目录，安装依赖
```shell
cd easy-mock-dev
npm install
```
6. 执行构建
```shell
npm run build
```
7. 启动
```shell
npm run start
```
8. EasyMack 端口号7300, 阿里云要开放7300
9. 打开浏览器 http://mengxuegu.com:7300