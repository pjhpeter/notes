### 热部署不起作用
原因是webpack监听的目录太小，当app的目录太多是有的就监听不到，默认为8192
```
cat /proc/sys/fs/inotify/max_user_watches

8192
```
可以修改为更大的值
```
echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p
```
修改成功，重启一下vscode就行
```
cat /proc/sys/fs/inotify/max_user_watches
524288
```