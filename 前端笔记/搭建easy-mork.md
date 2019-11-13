easy-mock要用nodejs启动，需要先安装nodejs
```
ubuntu系统：
自己下载8.x版本的nodejs，+++一定要8.x版本的！！+++ 
centos系统：
curl --silent --location https://rpm.nodesource.com/setup_8.x | bash -
yum install node
```
easy-mock依赖mongo和redis，需要确保服务器安装了mongo和redis，可以通过docker方式安装
```
ubuntu系统：
apt install docker.io
centos系统：
yum install docker
```
安装mongo
```
docker pull mongo
docker run --name mongo -p 27017:27017 -d mongo
```
easy-mock代码在github上，需要先安装git工具用于拉取代码
```
ubuntu系统：
apt install git
centos系统：
yum install git
```
从github上将easy-mock代码拉取下来
```
cd /home
git clone https://github.com/easy-mock/easy-mock.git
```
运行完之后代码就会下载到/home/easy-mock目录 
下载npm相关的依赖包
```
cd /home/easy-mock
npm install
```
使用node直接运行easy-mock有个问题，easy-mock是在前台运行，如果会话退出了，进程也就退出了。为了保证进程能够一直运行，可以使用pm2后台启动进程。
安装pm2
```
npm install pm2 -g
```
启动easy-mock
```
cd /home/easy-mock
pm2 start app.js
```