## 安装mysql8.0.12
### 下载
mysql
https://cdn.mysql.com//archives/mysql-8.0/mysql-server_8.0.12-1ubuntu18.04_amd64.deb-bundle.tar
相关的东西
https://pkgs.org/download/libtinfo5
http://security.ubuntu.com/ubuntu/pool/universe/m/mecab/libmecab2_0.996-5_amd64.deb
### 安装
解压
```
tar -xvf mysql-server.......
```
安装相关的东西和安装mysql的命令都是下面这个
```
sudo dpkg -i xxxxxxxx
```
mysql安装顺序如下：

1. mysql-common 

2. libmysqlclient20

3. libmysqlclient-dev

4.libmysqld-dev

5. mysql-community-client

6. mysql-client

7. mysql-community-source

8. mysql-community-server

中间会出现有两个选项，一定要选择第二个，5.x什么的那一项