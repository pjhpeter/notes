### 耳机没声音
下载pavucontrol软件：
```
sudo apt install pavucontrol
```
在终端执行命令打开软件
```
pavucontrol
```
按照下面配置 （可能每次开机都要配，可能不用）<br>
![输入图片说明](https://images.gitee.com/uploads/images/2019/1204/111602_493c31c3_5449551.png "屏幕截图.png")<br>
![输入图片说明](https://images.gitee.com/uploads/images/2019/1204/111740_f3d57976_5449551.png "屏幕截图.png")
### 启动tomcat报权限不够
原因是linux系统非root用户不能访问1024以下的端口，所以服务想用80端口启动时会报错，处理方式如下
```
iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-port 8080
```