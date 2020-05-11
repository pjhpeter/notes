### 环境
CentOS8、JDK8、ActiveMQ5.15.12

### 步骤
1. 下载ActiveMQ
```cmd
wget -c https://mirrors.tuna.tsinghua.edu.cn/apache//activemq/5.15.12/apache-activemq-5.15.12-bin.tar.gz
```
2. 解压
```cmd
tar -zxvf apache-activemq-5.15.12-bin.tar.gz -C /var
mv /var/apache-activemq-5.15.12/ /var/activemq/
```
> 这时就可以启动了

```cmd
/var/activemq/bin/activemq start
```
> 网页访问，默认端口是8161
>
> http://ip:8161/admin
> 
>用户名和密码都是admin
>
> 如果访问不了，记得关闭防火墙或者放行端口8161和61616

放行端口
```cmd
firewall-cmd --zone=public --add-port=8161/tcp --permanent
firewall-cmd --zone=public --add-port=61616/tcp --permanent
firewall-cmd --reload
```

3. 做成服务
方便运维人员部署，最好做成服务，创建文件/usr/systemd/system/activemq.service
```cmd
vim /usr/systemd/system/activemq.service
```
写入一下内容：
```
[Unit]
Description=ActiveMQ service
After=network.target


[Service]
Type=forking
ExecStart=/var/activemq/bin/activemq start
ExecStop=/var/activemq/bin/activemq stop
User=root
Group=root
Restart=always
RestartSec=9
StandardOutput=syslog
StandardError=syslog
SyslogIdentifier=activemq


[Install]
WantedBy=multi-user.target
```

4. 用找出java命令的目录
```cmd
whereis java
```

5. 修改ActiveMQ的配置文件
```cmd
vim /var/activemq/bin/env
```
将JAVA_HOME的路径写到配置文件的JAVA_HOME参数中
```
# (set JAVACMD to "auto" for automatic detection)
JAVA_HOME="/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.252.b09-2.el8_1.x86_64"
```

6. 重新加载服务配置
```cmd
systemctl daemon-reload
```

7. 启动服务
```cmd
systemctl start activemq
```

8. 设置开机自启动
创建链接
```cmd
ln -s /usr/lib/systemd/system/activemq.service /etc/systemd/system/multi-user.target.wants/activemq.service
```
开机自启
```cmd
systemctl enable activemq
```
检查是否添加开机自启成功
```cmd
systemctl list-unit-files | grep activemq
```

